<script>
export default {
    props: ['pokemonList'],
    data() {
        return {
            capturedPokemon: [],
        };
    },
    mounted() {
        this.loadCapturedPokemon();
    },
    methods: {
        loadCapturedPokemon() {
            const keys = Object.keys(localStorage);
            this.capturedPokemon = keys.map(key => JSON.parse(localStorage.getItem(key)));
        },
        selectPokemon(pokemon) {
            this.$emit('pokemon-selected', pokemon);
        }
    }
}

</script>

<template>
<div class="container rounded-4 mt-3 pokedex">
    <h3>Il tuo Pokedex</h3>
    <ul class="d-flex">
        <li v-for="pokemon in pokemonList" :key="pokemon.name" @click="selectPokemon(pokemon)" >
              <img :src="pokemon.sprites.front_default" :alt="pokemon.name">
        </li>
    </ul>
</div>

</template>


<style lang="scss" scoped>
.pokedex {
    background-color: white;
    // debug
    height: 470px;
}

li {
    list-style-type: none;
    cursor: pointer;
}

</style>