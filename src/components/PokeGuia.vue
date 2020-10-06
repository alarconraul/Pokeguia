<template>
  <div>
      <h1>Poke Guía</h1>
      <p>Nombre</p>
      <input v-model="pokemonName" type="text">
      <button @click="searchPoke">Buscar</button>
      <img :src="currentPokemon.sprites.front_default">
      
      <h3>Moves</h3>
      <ul>
          <li v-for="move in moves" :key="move.name">
              {{move.move.name}}
          </li>
      </ul>
      
      <h3>Abilities</h3>
      <ul>
          <li v-for="ability in abilities" :key="ability.name">
              {{ability.ability.name}}
          </li>
      </ul>
  </div>
</template>

<script>
export default {
    data() {
        return {
            currentPokemon: {},
            pokemonName: ""
        }
    },

    created() {
            fetch(`https://pokeapi.co/api/v2/pokemon/pikachu`) 
            .then(response => response.json()) 
            .then(data => this.currentPokemon = data)
    },

    methods: {
        searchPoke () {
            fetch(`https://pokeapi.co/api/v2/pokemon/${this.lower}`) 
            .then(response => response.json()) 
            .then(data => this.currentPokemon = data)
        }
    },

    computed: {
        moves() {
            return this.currentPokemon.moves
        },

        abilities() {
            return this.currentPokemon.abilities
        },
        lower(){
          return this.pokemonName.toLowerCase()
        }
    }
    
}
</script>

<style>

</style>