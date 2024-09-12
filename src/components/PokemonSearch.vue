<script>
import axios from 'axios';

export default {
    data() {
        return {
            pokemon: '',
            error: null,
        };
    },
    methods: {
        searchPokemon() {
            if (!this.pokemon) return;

            axios
            .get(`https://pokeapi.co/api/v2/pokemon/${this.pokemon.toLowerCase()}`)
            .then((resp) => {
                console.log(resp.data);
                this.$emit('pokemon-found', resp.data);
                this.error = null;
                
            })
            .catch(() => {
                this.error = 'Pokemon non trovato!';
            });
        },
    },
};

</script>

<template>

    <div class="container">
        <input v-model="pokemon" placeholder="Cerca un Pokémon..." @keyup.enter="searchPokemon" />
        <button @click="searchPokemon">Cerca</button>
        <p v-if="error">{{ error }}</p>
    </div>

</template>


<style lang="scss" scoped></style>