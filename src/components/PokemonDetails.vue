<script>
export default {
    props: ['pokemon'],
    mounted() {
        console.log(this.pokemon);
    },
    computed: {
        isCaptured() {
            return localStorage.getItem(this.pokemon.name) !== null;
        },
    },
    methods: {
        catchPokemon() {
            localStorage.setItem(this.pokemon.name, JSON.stringify(this.pokemon));
            // console.log(localStorage);
            this.$emit('catch-pokemon');
            
        },
        releasePokemon() {
            localStorage.removeItem(this.pokemon.name);
            this.$emit('release-pokemon');
        },
    },
};


</script>

<template>
    <div class="container" v-if="pokemon">
        <h2>{{  pokemon.name.toUpperCase() }}</h2>
        <img :src="pokemon.sprites.front_default" :alt="pokemon.name">
        <p>Tipo: {{ pokemon.types.map(t => t.type.name).join(', ') }}</p>
        <button @click="catchPokemon">Cattura</button>
        <button @click="releasePokemon" v-if="isCaptured">Libera</button>
    </div>

</template>


<style lang="scss" scoped></style>