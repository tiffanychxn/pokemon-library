<template>
   <br>
   <label>PAGES</label>
   <br>
   <button type="button" class="action" @click="this.$parent.prevPage()">PREV</button>
   <template v-bind:key="index" v-for="(pokemon, index) in paginationPages">
      <button v-if="this.$parent.currentPage==index" type="button" class="action-select" @click="this.$parent.navigatePage(index)">{{index+1}}</button>
      <button v-else type="button" class="action" @click="this.$parent.navigatePage(index)">{{index+1}}</button>
   </template>
   <button type="button" class="action" @click="this.$parent.nextPage()">NEXT</button>
   <label class="subtext">CURRENTLY DISPLAYING POKÉMON {{this.$parent.currentPage*30+1}} - {{this.$parent.currentPage*30+30}}</label>
</template>

<script>
import '../assets/style.css';
export default {
  name: 'navigationPagnation',
  props:['paginationPages']
}
</script>
