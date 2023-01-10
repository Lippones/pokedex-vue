<template>
  <div class="app p-5 d-flex justify-content-center row">
    <div class="headerr">
      <img src="/title.png" class="w-25 mb-2"/>
      <input type="text" placeholder="Digite o nome do pokemon" v-model="busca" class="form-control w-25 input">
      <button class="btn btn-primary mb-4 w-25" @click="buscaPoke">Buscar</button>
    </div>
    <div class="container-s ">
      <div class="w-25 mb-2 d-inline-flex" v-for="(poke,index) in filteredPokemons" :key="poke.name">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>
  </div>
</template>
<script>
import Pokemon from './components/Pokemon.vue'
import axios from 'axios'
export default{
  data(){
    return{
      pokemons:[],
      filteredPokemons:[],
      busca:''
    }
  },
  created:async function(){
    try{
      const res = await axios.get('https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0')
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results
    }catch(err){
      console.log(err)
    }
  },
  components:{
    Pokemon,
  },methods:{
    buscaPoke:function(){
      if(this.busca == '' || this.busca == ''){
        this.filteredPokemons = this.pokemons
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon=> pokemon.name == this.busca.toLowerCase())
      }
    }
  },
  computed:{
    /*buscaPoke:function(){
      if(this.busca == '' || this.busca == ''){
        return this.pokemons
      }else{
        return this.pokemons.filter(pokemon=> pokemon.name == this.busca)
      }
    }*/
  }
}
</script>
<style scoped>
  .app{
    height: 100vh;
    background-image: url('/fundo.png');
  }
  .input{
    width:80%;
    margin:20px 0;
  }
  .headerr {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>
