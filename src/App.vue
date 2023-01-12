<template>
    <div class="container">
      <div id="info">
          <h1 class="title is-1 has-text-danger">Sobre Pokémons</h1>
          <p class="has-text-danger title is-4">
            Este é seu site de informações rápidas sobre seus Pokémons preferidos! Saiba qual é o tipo e suas possíveis evoluções.
          </p>
      </div>

      <div v-for="(poke,index) in pokemons" :key="index">
          <Pokemon :name="poke.name" :url="poke.url" :index="index + 1"></Pokemon>
      </div>
    </div>
</template>

<script>
//Imports
import axios from 'axios';
import Pokemon from './components/Pokemon.vue';

export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
    }
  },
  created: function() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      console.log('Pegou a lista de pokemon');
      this.pokemons = res.data.results;   
    })
  }, 
  components: {
    Pokemon
  }
}
</script>

<style scoped>
#info {
  width: 480px;
  padding-top: 100px;
}
</style>
