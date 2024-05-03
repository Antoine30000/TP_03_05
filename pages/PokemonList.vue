<template>
    <div>
      <h1>List of Pokémon Cards</h1>
      <div v-if="loading">Loading...</div>
      <div v-else>
        <div v-for="pokemon in pokemonList" :key="pokemon.id">
          <div>{{ pokemon.name }}</div>
          <img :src="pokemon.imageUrl" alt="pokemon" />
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        loading: true,
        pokemonList: []
      };
    },
    async fetch() {
      try {
        const response = await this.$fetch('https://api.pokemontcg.io/v2/pokemon?limit=10&offset=0');
        this.pokemonList = response.data.data;
        this.loading = false;
      } catch (error) {
        console.error('Error fetching Pokémon data:', error);
      }
    }
  };
  </script>
  
  <style>
  
  </style>
  