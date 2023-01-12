<template>
    <div class="container column is-half is-offset-one-quarter">
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

</style>
