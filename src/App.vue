<template>
   <nav id="topo" class="navbar" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <a class="navbar-item">
        <img id="logo" src="./assets/International_Pokémon_logo.svg.png" alt="Pokémon" >
      </a>

      <a role="button" class="navbar-burger" aria-label="menu" aria-expanded="false">
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
      </a>
    </div>
  </nav>
    <div class="container" id="caixa">
      <div id="info">
          <h1 class="title is-3 has-text-danger">Sobre Pokémons</h1>
          <p class="has-text-danger title is-5">
            Este é seu site de informações rápidas sobre seus Pokémons preferidos! Saiba qual é o tipo e suas possíveis evoluções.
          </p>
      </div>

      <div id="search">
          <label for="pokemon" class="label has-text-danger">Pesquisar por Pokémon</label>
          <input v-model="busca" type="text" name="pokemon" id="pokemon" class="input is-danger" placeholder="Entre com o nome do pokemon" >
          <button class="button is-fullwidth is-rounded is-danger" id="btnBusca"  @click="buscar">Pesquisar</button>
      </div>

      <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
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
      filteredPokemons: [],
      busca: '',
    }
  },
  created: function() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      console.log('Pegou a lista de pokemon');
      this.pokemons = res.data.results;   
      this.filteredPokemons = res.data.results;
    })
  }, 
  components: {
    Pokemon,
  },

  methods: {
    buscar: function() {
      this.filteredPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ' ' || this.busca == undefined){
        this.filteredPokemons = this.pokemons;
      }
      else {
        this.busca = this.busca.toLocaleLowerCase();
        this.busca = this.busca.trim();
        this.filteredPokemons = this.pokemons.filter(poke =>  poke.name === this.busca);
        console.log(this.filteredPokemons);
      }
    }
  },  

  computed: {
   /*  resultadoBusca: function() {
      if(this.busca == '' || this.busca == ' '){
        return this.pokemons;
      }
      else {
        return this.pokemons.filter(pokemons => pokemons.name == this.busca);
      }
    } */
  }
}
</script>

<style scoped>
#info {
  width: 480px;
  padding-top: 300px;
}

#search {
  background-color: none;
  padding: 20px;
  width: 480px;
}

#btnBusca {
  margin-top: 15px;
}

#topo {
  height: 150px;
  background: rgba(0, 0, 255, 0.378);
  position: fixed;
  top: 0;
  left: 0; 
  width: 100%;
}


</style>
