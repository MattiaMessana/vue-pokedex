<script>
import PokemonSearch from './components/PokemonSearch.vue';
import PokemonDetails from './components/PokemonDetails.vue';

export default {
  components: {
    PokemonSearch,
    PokemonDetails
  },
  data() {
    return {
      selectedPokemon: null,
    };
  },
  methods: {
    showPokemon(pokemon) {
      this.selectedPokemon = pokemon;
    },
  },
};
</script>

<template>
  <PokemonSearch @pokemon-found="showPokemon" />
  <PokemonDetails v-if="selectedPokemon" :pokemon="selectedPokemon" />
</template>

<style lang="scss">

</style>
