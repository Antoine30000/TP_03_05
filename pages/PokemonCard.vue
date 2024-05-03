<script>
export default {
  async asyncData({ params }) {
    try {
      const response = await $fetch(`https://pokeapi.co/api/v2/pokemon/${params}`);
      return { pokemon: response };
    } catch (error) {
      console.error('Error while loading pokemon info :', error);
      return { pokemon: null };
    }
  }
};
</script>

<template>
    <div>
      <h1>{{ pokemon.name }}</h1>
      <div>
      </div>
      <div>
        <h2>Abilities:</h2>
        <ul>
          <li v-for="(ability, index) in pokemon.abilities" :key="index">{{ ability.name }}</li>
        </ul>
      </div>
    </div>
  </template>
  
 
  