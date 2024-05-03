<script>
export default {
  data() {
    return {
      loading: true,
      pokemonList: []
    };
  },
  async mounted() {
    try {
      const response = await $fetch('https://pokeapi.co/api/v2/pokemon?limit=10&offset=0');
      this.pokemonList = response.results;
      this.loading = false;
    } catch (error) {
      console.error('Error while loading pokemons :', error);
    }
    console.log(this.pokemonList)
  }
};


</script>

<template>
  <div>
    <h1>Liste des Pokémon</h1>
    <div v-if="loading">Loading...</div>
    <div v-else>
      <div v-for="pokemon in pokemonList" :key="pokemon.id">
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

  

  
  