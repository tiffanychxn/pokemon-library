<template>
    <navigation-scroll  v-bind:offset="offset"/>
    <ul class="cards">
    <div v-bind:key="index" v-for="(pokemon, index) in $parent.scrollArray">
        <pokemon-card v-bind:pokemon="pokemon"/>
    </div>
    </ul>
    <navigation-scroll v-bind:offset="offset"/>
</template>

<script>
import pokemonCard from '../components/pokemonCard.vue'
import navigationScroll from '../components/navigationScroll.vue'
import '../assets/style.css';

export default {
  name: 'displayScroll',
  components: {
    pokemonCard,
    navigationScroll,
  },
  data(){
    return{
      //offset of increments used in load more
      offset:50,
    }
  },
  methods:{

  loadMorePokemon(){
      //increment the pokemon added by 15 or 10 , if the offset number is not over 140
      if(this.offset <=140){
        let offsetIncrement = 15
        if(this.offset==140){
          offsetIncrement = 10
        }
        //take desired pokemon to be added to the scroll Array
        let morePokemon = this.$parent.pokedexArray.slice(this.offset,this.offset+offsetIncrement)
        this.$parent.scrollArray = this.$parent.scrollArray.concat(morePokemon)
        //increment offset
        this.offset+=offsetIncrement  
      }
    },
  
  viewLessPokemon(){
    //decrement the offset by 15 or 10, only if the offset number is 65 or more
      if(this.offset >=65){
        let offsetDecrement = 15
        if(this.offset==150){
          offsetDecrement = 10
        }
        //decrement offset
        this.offset-=offsetDecrement
        //remove desired amount of pokemon from scroll array
        let arrayLen = this.$parent.scrollArray.length
        this.$parent.scrollArray.splice(arrayLen-offsetDecrement,arrayLen)
      }
  }
      
  }

  
}
</script>
