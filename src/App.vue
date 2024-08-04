<script>
import axios from 'axios';
import CardPokemon from './components/CardPokemon.vue';

export default {
  components: {
    CardPokemon,
  },
  data() {
    return {
      url: 'https://pokeapi.co/api/v2/pokemon',
      pokemones:[],      
      contadorAciertos: 0,  
    }
  },  
  methods: {  
    async getPokemones() {
      try {
        const {data} = await axios.get(`${this.url}?limit=20`) /*llamado a la api */
        const listaPokemones = await data.results;
        listaPokemones.forEach(async (pokemon,index)=>{
          
          const {data} = await axios.get(`${this.url}/${index + 1}/`)
          const {name, sprites: {other: {dream_world: {front_default}}}} = data
          const pokemonObject = {name, img:front_default }
          
          return this.pokemones.push(pokemonObject) 
        })              
      } catch (error) {
        this.error=error;
        alert('Error obteniendo la lista de pokemones:', error);
      }
    },
    revelarPokemon(index){
      this.pokemones[index].visible=true;
      this.contadorAciertos++;
    }
  },
  mounted() {
    this.getPokemones();
  },
}
</script>

<template>
  <div class="contenedor">
    <div class="titulo">
      <img src="../public/pokemon.png" alt="">
      <h1>¿Quién es ese Pokémon?</h1>
      <div class="contador-pokemon">
        <h4>Pokemones descubiertos:</h4> 
        <p>{{ contadorAciertos }}</p>
      </div>
    </div>

    <div class="card-pokemones-todos">
      <card-pokemon 
      v-for="(pokemon, index) in pokemones" 
      :key="index" :pokemon="pokemon"
      @respuestaCorrecta="revelarPokemon(index)" />
    </div>
  </div>

</template>

<style>
*{
  margin: 0;
  padding: 0;
  border: 0;
  box-sizing: 0;
  background-color: #f9ffd7;
}
.contenedor{  
  margin: auto;
  padding: 1rem;
}
.card-pokemones-todos{
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 0.5rem;

  margin: auto;
  
}
.titulo{
text-align: center;
text-shadow: 1px 1px 20px #567eff;
}
.titulo img{
width: 20rem;
}
.contador-pokemon{
  display: flex;
  align-items: center;
  justify-content: center;

  margin: 1rem; 
}
.contador-pokemon h4{
  padding-right: 1rem;
}
p h4{
  font-weight: 500;
  font-size: large;
  text-align: center;
}
p{
  color: #c40000;
  font-weight: bolder;
  font-size: x-large;
}
</style>