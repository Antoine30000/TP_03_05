 <script>
async function getPokemon(){
    const pokemon = await $fetch('https://pokeapi.co/api/v2/pokemon?limit=10&offset=0')
}
console.log(getPokemon())
  </script>

  <template>
    <div>
      <h1>List of Pokémon Cards</h1>
      <div v-if="loading">Loading...</div>
      <div v-else>
        <div v-for="pokemon in pokemonList" :key="pokemon.id">
          <div>
            <h2>{{ pokemon.name }}</h2>
            <ul>
              <li v-for="(ability, index) in pokemon.abilities" :key="index">{{ ability.name }}</li>
            </ul>
            <img :src="pokemon.images.small" alt="pokemon" />
          </div>
        </div>
      </div>
    </div>
  </template>
  
 
  

  
  