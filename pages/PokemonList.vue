<script>
export default {
  data() {
    return {
      loading: true,
      pokemonList: [],
      searchQuery: '',

    };
  },
  async mounted() {
    try {
      const response = await $fetch('https://pokeapi.co/api/v2/pokemon?limit=151');
      this.pokemonList = response.results;
      this.loading = false;
    } catch (error) {
      console.error('Erreur lors de la récupération des Pokémon :', error);
    }
  },
  computed: {
    filteredPokemonList() {
      return this.pokemonList.filter(pokemon => pokemon.name.toLowerCase().includes(this.searchQuery.toLowerCase()));
    }
  },
  methods: {
    goToPokemonDetails(pokemonName) {
      navigateTo(`/PokemonCard/${pokemonName}`)
    }
  }
};
</script>

<template>
  <div>
    <h1>Pokédex</h1>
    <input type="text" v-model="searchQuery" placeholder="Rechercher un Pokémon..." />
    <div v-if="loading">Loading...</div>
    <div v-else>
      <div v-for="(pokemon, index) in filteredPokemonList.slice(0, 10)" :key="index" @click="goToPokemonDetails(pokemon.name)">
        <div>
          <h2>{{ pokemon.name }}</h2>
          <ul>
            <li v-for="(ability, index) in pokemon.abilities" :key="index">{{ ability.name }}</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>