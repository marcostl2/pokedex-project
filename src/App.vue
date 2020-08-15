<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h1 class="is-size-1">Pokédex</h1>
      <input
        type="text"
        placeholder="Buscar pokémon pelo nome"
        v-model="busca"
        class="input is-rounded"
      />
      <a 
      @click="buscar"
        class="button is-link" 
        style="width:200px;margin: 25px 0;"
      >Buscar</a>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      filteredPokemons:[],
      busca: "",
    };
  },
  created: async function() {
    const url = "https://pokeapi.co/api/v2/pokemon?limit=151&offset=0";
    const pokemonsList = await axios.get(url);
    this.pokemons = pokemonsList.data.results;
    this.filteredPokemons = pokemonsList.data.results;
  },
  components: {
    Pokemon,
  },
  methods:{
    buscar:function(){
      this.filteredPokemons= this.pokemons
      if(this.busca==''||this.busca==' '){
        this.filteredPokemons= this.pokemons
      }else{
        this.filteredPokemons= this.pokemons.filter(pokemon=>pokemon.name==this.busca)
      }
    }
  },
  computed:{
    // resultadoBusca:function(){
    //   if(this.busca==''||this.busca==' '){
    //     return this.pokemons
    //   }else{
    //     return this.pokemons.filter(pokemon=>pokemon.name==this.busca)
    //   }
    // }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap");

* {
  margin: 0;
  padding: 0;
  font-family: "Poppins", sans-serif;
  box-sizing: border-box;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
