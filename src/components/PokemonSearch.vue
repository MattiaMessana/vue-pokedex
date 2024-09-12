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
            if (!this.pokemon.trim()) {
                this.error = 'Inserisci il nome del Pokemon';
                return;
            };

            

            axios
                .get(`https://pokeapi.co/api/v2/pokemon/${this.pokemon.toLowerCase()}`)
                .then((resp) => {
                    console.log(resp.data);
                    this.$emit('pokemon-found', resp.data);
                    this.error = null;
                    this.pokemon = '';

                })
                .catch(() => {
                    this.error = 'Pokemon non trovato!';
                });
        },
    },
};

</script>

<template>

    <div class="container mt-3">
        <div class="row">
            <div class="col">
                <div class="input-group input-group-sm">

                    <input placeholder="Cerca un pokemon..." type="text" class="form-control" v-model="pokemon"
                        @keyup.enter="searchPokemon" />

                    <button class="btn btn-light mx-1" @click="searchPokemon">
                        <i class="fa-solid fa-magnifying-glass fa-sm"></i>
                    </button>
                </div>
            </div>

            <p class="mt-4" v-if="error">{{ error }}</p>
        </div>
    </div>

</template>


<style lang="scss" scoped></style>