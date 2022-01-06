<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <div class="is-flex is-flex-direction-row">
        <input class="input is-rounded" type="text" placeholder="Busque seu pokemon" v-model="busca">
        <div class="separar"></div>
        <button class="button is-success is-rounded" @click="clickSearch">Buscar</button>
      </div>
      <p v-for="(poke,index) in filteredArray" :key="poke.url">
        <pokemon :pokemon="poke" :num="index + 1"/>
      </p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import pokemon from './components/pokemon'
export default {
  name: 'App',
  components :{
    pokemon
  },
  data(){
    return{
      busca: "",
      filteredArray : [],
      pokemons : []
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res =>{
      console.log("pegou a lista de pokemons")
      this.pokemons = res.data.results
      this.filteredArray = this.pokemons
    })
  },
  methods:{
    clickSearch : function(){
      this.filteredArray = this.pokemons
      if(this.busca == ' ' || this.busca == ''){
        this.filteredArray = this.pokemons
      }else{
        this.filteredArray = this.pokemons.filter(monstro => monstro.name == this.busca)
        console.log(this.filteredArray)
      }
    }
  },
  computed:{
    // returnSearch : function(){
    //   if(this.busca == ' ' || this.busca == ''){
    //     return this.pokemons
    //   }else{
    //     return this.pokemons.filter(monstro => monstro.name == this.busca)
    //   }
    // }
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
  .separar{
    margin-left: 1%;
  }
</style>
