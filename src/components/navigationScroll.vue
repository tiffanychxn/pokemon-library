<template >    
  <br>
  <button v-if="offset<150" type="button" class="action" @click="this.$parent.loadMorePokemon">LOAD MORE</button>
  <button v-if="offset>50" type="button" class="action" @click="this.$parent.viewLessPokemon">VIEW LESS</button>
  <label class="subtext">CURRENTLY DISPLAYING {{offset}} OUT OF 150 POKÉMON</label>  
</template>

<script>
import '../assets/style.css';
export default {
  name: 'navigationScroll',
  props: ['offset']
}
</script>
