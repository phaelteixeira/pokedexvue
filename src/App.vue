<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <p class="is-size-4">Pokedex</p>
      <input class="input is-rounded" type="text" placeholder="Buscar pokemon pelo nome" v-model="busca"/>
      <button class="button is-fullwidth is-dark" id="buscaBtn" @click="buscar">Buscar</button>
      <div v-for="(pokemon,index) in filteredPokemons" :key="pokemon.url">
        <Pokemon :id="index" :name="pokemon.name" :url="pokemon.url"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from '../src/components/Pokemon.vue';

export default {
  name: 'App',
  components:{
    Pokemon
  },
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then( res => {
      console.log('Pokemons coletados.');
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    }).catch( err => {
      console.log(err);
    });
  },
  methods: {
    buscar: function() {
      this.filteredPokemons = this.pokemons;
      if (this.busca == '' || this.busca == ' ') {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter( pokemon => pokemon.name == this.busca.toLowerCase());
      }
    }
  },
  computed: {
      
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#buscaBtn {
  margin-top: 2%;
  margin-bottom: 8%;
}
</style>
