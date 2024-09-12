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
    <div class="container mt-5" v-if="pokemon">
        <div class="row">
            <h2>{{  pokemon.name.toUpperCase() }}</h2>

            <div class="col bgDetails">
                <img :src="pokemon.sprites.front_default" :alt="pokemon.name">
            </div>
            
            <p class="mt-3">Tipo: {{ pokemon.types.map(t => t.type.name).join(', ') }}</p>
            
            <div class="col">
                <button class="btn btn-success me-2"  @click="catchPokemon">Cattura</button>
                <button class="btn btn-warning" @click="releasePokemon" v-if="isCaptured">Libera</button>
            </div>
        </div>
    </div>

</template>


<style lang="scss" scoped>
h2 {
    color: white;
}
.bgDetails {
    background-color: gray;
    img {
        width: 150px;
        background-color: white;
    }
}
</style>