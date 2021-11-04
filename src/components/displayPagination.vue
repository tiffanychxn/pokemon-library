<template>
    <navigation-pagination v-bind:paginationPages="this.$parent.paginationPages"/>
    <ul class="cards">
        <template v-bind:key="index" v-for="(pokemon, index) in this.$parent.paginationArray">
            <pokemon-card v-bind:pokemon="pokemon"/>
        </template>
    </ul>
    <navigation-pagination v-bind:paginationPages="this.$parent.paginationPages"/>
</template>

<script>
import pokemonCard from './pokemonCard.vue'
import navigationPagination from './navigationPagination.vue'
import '../assets/style.css';

export default {
  name: 'displayPagination',
  components: {
    pokemonCard,
    navigationPagination,
  },
  data(){
    return{
      //current page user is on
      currentPage:0
    }
  },
  methods:{
  
  navigatePage(selectedPage){
    //set current page to selected page
    this.currentPage = selectedPage
    //determine which pokemon should be on page. for example, if page 2 is selected, pokemon #31 - #60 should be displayed
    let pokemonOnPage = selectedPage*30 
    this.$parent.paginationArray = this.$parent.pokedexArray.slice(pokemonOnPage,pokemonOnPage+30)
  },

  nextPage(){
    //navigate to next page, if page number does not exceed index of 4
    if(this.currentPage<4){
      this.navigatePage(this.currentPage+1)
    }
  },

  prevPage(){
    //navigate to prev page, if page number does not go below index of 0
    if(this.currentPage>0){
      this.navigatePage(this.currentPage-1)
    }
  },
  }

}
</script>
