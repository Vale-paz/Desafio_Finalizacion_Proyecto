<script>
import InputNombrePokemon from './InputNombrePokemon.vue';

export default {
    props: {
        pokemon: {
            type: Object,
            required: true,
        }
    },
    components: {
        InputNombrePokemon,
    }
}
</script>

<template>
    <div class="card"> 
        <div class="card-pokemon" 
        :style="{ filter: pokemon.visible ? 'none' : 'blur(5px) grayscale(100%)' }">
            <img class="card-pokemon_img" :src="pokemon.img" :alt="pokemon.name">
        </div>
        <input-nombre-pokemon 
        v-if="!pokemon.visible" 
        :pokemon="pokemon"
        @respuestaCorrecta="$emit('respuestaCorrecta')" 
        />
        <div v-else>
            <h4>{{ pokemon.name }}</h4>
        </div>
    </div>
</template>

<style scoped>
.card{    
    box-shadow: 1px 1px 10px 1px #888888;
    border-radius: 5px;

    margin: 1rem 1rem;
}
.card-pokemon { 
    width: 10rem;
    margin: 1rem;
    padding: 10px;
    border:1px solid #310000;
    

}
.card-pokemon_img{
    width: 9rem;
    height: 8rem;
    display: flex;
    align-items: center;
    justify-content: center;
    
}
h4{
    text-align: center;
    color: #3f3f3f;
    font-size: large;
    font-weight: 900;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    text-shadow: 1px 1px 20px #567eff;
}
</style>