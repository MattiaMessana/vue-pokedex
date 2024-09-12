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
<div class="container">
    <h3>Il tuo Pokedex</h3>
    <ul>
        <li v-for="pokemon in pokemonList" :key="pokemon.name" @click="selectPokemon(pokemon)" >
            {{ pokemon.name }}
        </li>
    </ul>
</div>

</template>


<style lang="scss" scoped>

</style>