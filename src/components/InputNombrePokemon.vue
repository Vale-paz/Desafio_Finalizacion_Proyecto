<script>
export default {
    props: {
        pokemon: {
            type: Object,
            required: true,
        }
    },
    data() {
        return {
            nombrePokemonUsuario: '',
        }
    },
    methods: {
        descubrirPokemon() {
            if (this.pokemon.name.toLowerCase() === this.nombrePokemonUsuario.toLowerCase()) {
                this.$emit('respuestaCorrecta');
            } else {
                this.$emit('respuestaIncorrecta');
            }
            this.nombrePokemonUsuario = '';
        },
    }
}
</script>

<template>
    <div class="ingresar-datos">
        <input v-model="nombrePokemonUsuario" type="text">
        <button @click="descubrirPokemon">Descubrir</button>
    </div>
</template>

<style scoped>
.ingresar-datos{
    margin: 1rem 0 ;
    display: flex;
    flex-direction: column;
    align-items: center;
}
button{
    background-color: #4543c5;
    color:#fff;
    border: 1px solid #525050;

    border-radius: 5px;
    margin: .5rem 0 ;
    width:10.8rem;
    height: 1.5rem;
}
input{
    border: 1px solid #3f3f41;
    border-radius: 5px;
    text-align: center;
}
</style>