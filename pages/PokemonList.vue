<script>
export default {
  data() {
    return {
      loading: true,
      pokemonList: [],
      searchQuery: ''
    };
  },
  async mounted() {
    try {
      const response = await $fetch('https://pokeapi.co/api/v2/pokemon?limit=151'); // Fetching first 151 Pokémon
      this.pokemonList = response.results;
      this.loading = false;
    } catch (error) {
      console.error('Erreur lors de la récupération des Pokémon :', error);
    }
  },
  computed: {
    filteredPokemonList() {
      return this.pokemonList.filter(pokemon => {
        return pokemon.name.toLowerCase().includes(this.searchQuery.toLowerCase());
      });
    }
  },
  methods: {
    goToPokemonDetails(pokemonName) {
      this.$router.push(`/pokemon/${pokemonName}`);
    }
  }
};
</script>

<template>
  <div>
    <h1>Liste des Pokémon</h1>
    <input type="text" v-model="searchQuery" placeholder="Rechercher un Pokémon..." />
    <div v-if="loading">Chargement...</div>
    <div v-else>
      <div v-for="pokemon in filteredPokemonList" :key="pokemon.id" @click="goToPokemonDetails(pokemon.name)">
        <div>
          <h2>{{ pokemon.name }}</h2>
          <ul>
            <li v-for="(ability, index) in pokemon.abilities" :key="index">{{ ability.name }}</li>
          </ul>
          <img :src="`https://pokeres.bastionbot.org/images/pokemon/${pokemon.id}.png`" alt="pokemon" />
        </div>
      </div>
    </div>
  </div>
</template>