<template>
   <div>
      <div class="page-nav">
        <img height="100" src="./assets/pokemon-logo.png">
        <br>
         <label for="pageType">CHOOSE A TYPE OF DISPLAY: </label>
         <select class="action" v-model="pageType">
            <option value="pagination">PAGINATION</option>
            <option value="scroll">SCROLL</option>
         </select>
         <p>HOVER OVER THE POKÉMON NAMES TO DISPLAY HEIGHT AND WEIGHT.</p>
      </div>
      <displayPagination v-if="pageType=='pagination'"/>
      <displayScroll v-if="pageType=='scroll'"/>
      <loadingModal v-show="showModal"/>
   </div>
</template>

<script>
import displayPagination from './components/displayPagination.vue'
import displayScroll from './components/displayScroll.vue'
import loadingModal from './components/loadingModal.vue'
import axios from 'axios';
import './assets/style.css';
export default {
    name: 'App',
    components: {
        displayPagination,
        displayScroll,
        loadingModal
    },
    data() {
        return {
            //loading modal
            showModal:false,
            //page display type
            pageType: 'pagination',
            //max number of pokemon to be displayed
            maxPokemonDisplay: 150,
            //pages available in pagnation
            paginationPages: [],
            //dynamic array for pagination display
            paginationArray: [],
            //dynamic array for scroll/loading display
            scrollArray: [],
            //master array for all pokemon
            pokedexArray: []
            
        }
    },
    created() {
        this.showModal = true
        //initalize number of pages needed for pagination
        this.initPagination()
        //call pokeAPI to get all pokemon in the library
        this.getPokemon()

    },
    methods: {
        async getPokemon() {
            //get all 150 pokemon
            axios
                .get('https://pokeapi.co/api/v2/pokemon?limit=' + this.maxPokemonDisplay)
                .then(async function(response) {
                    //for each pokemon in the array of 150, get details and characteristics
                    for (const pokemon of response.data.results) {
                        //this api is called asynchonously, so that we can recieve the pokemon in order of ID
                        await this.getPokemonAttribute(pokemon.url)
                    }
                }.bind(this))
        },

        async getPokemonAttribute(pokemonURL) {
            //get all pokemon attributes
            await axios
                .get(pokemonURL)
                .then(response => {
                    let currentPokemon = response.data
                    //push data to master pokemon array
                    this.pokedexArray.push({
                        "id": currentPokemon.id,
                        "name": currentPokemon.name,
                        "image": currentPokemon.sprites.front_default,
                        "height": currentPokemon.height,
                        "weight": currentPokemon.weight
                    })
                    //once the last pokemon is processed, set up displays
                    if (currentPokemon.id == this.maxPokemonDisplay) {
                        //copy master pokemon array before processing
                        this.paginationArray = JSON.parse(JSON.stringify(this.pokedexArray))
                        //the first page of pagination should show 30 pokemon
                        this.paginationArray = this.paginationArray.splice(0, 30)

                        //copy master pokemon array before processing
                        this.scrollArray = JSON.parse(JSON.stringify(this.pokedexArray))
                        //the first page of scroll display should show 50 pokemon
                        this.scrollArray = this.scrollArray.splice(0, 50)

                        //close modal
                        this.showModal = false
                    }
                })
        },

        initPagination() {
          //determine number of pages in pagination
            for (var i = 0; i < this.maxPokemonDisplay / 30; i++) {
                this.paginationPages.push(i)
            }
        },

    }
}
</script>

<style>
#app {
  font-family: "VCR"  ;
  text-align: center;
  color: #cfd1d3;
}

</style>
