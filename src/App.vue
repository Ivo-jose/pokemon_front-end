<template>
    <div class="">
      <div v-for="(poke,index) in pokemons" :key="index">
          <h1>{{ index + 1 }}-{{ poke.name}} --- {{ poke.url }}</h1>
      </div>
    </div>
</template>

<script>
import axios from 'axios';
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
}
</script>

<style scoped>

</style>
