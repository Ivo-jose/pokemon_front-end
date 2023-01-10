<template>
    <div class="wrapper">
      <h1 class="title is-1">Teste</h1>
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
  }
}
</script>

<style scoped>
.wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
}
</style>
