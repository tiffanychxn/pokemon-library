<template>
  <li>
    <a class="card">
      <img :src="pokemon.image" class="card-image" alt="" />
      <div class="card-overlay">
        <div class="card-header">
            <p class="card-title">{{(pokemon.name).toUpperCase()}}</p>
        </div>
        <p class="card-description">HEIGHT: {{pokemon.height}} Decimetres <br> WEIGHT: {{pokemon.weight}} Hectograms</p>
      </div>
    </a>      
  </li>
</template>

<script>
import '../assets/style.css';
export default {
  name: 'pokemonCard',
  props: ['pokemon']
}
</script>
