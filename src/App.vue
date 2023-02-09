<template>
  <header>
    <a href="#"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/International_Pok%C3%A9mon_logo.svg/269px-International_Pok%C3%A9mon_logo.svg.png?20150121202211"></a>
  </header>

  <div class="searchArea">
    <h2>Digite o nome ou o ID do Pokemon desejado:</h2>
    <input type="text" v-model="inputValue" placeholder="Nome ou ID do Pokemon" autofocus/><br>
    <button @click="searchPokemon">Procurar Pokemon</button>
  </div>

    <div v-if="pokemon">
      <h2>{{ pokemon.name }}</h2>
      <p>Tipo: {{ pokemon.types.map(t => t.type.name).join(', ') }}</p>
      <img :src="pokemon.sprites.front_default" />

      <h3>Habilidades</h3>
      <ul>
        <li v-for="ability of pokemon.abilities">{{ ability.ability.name }}</li>
      </ul>

      <table>
        <tr>
          <th>HP:</th>
          <td>{{ pokemon.stats.find(s => s.stat.name === 'hp').base_stat }}</td>
        </tr>
        <tr>
          <th>Ataque:</th>
          <td>{{ pokemon.stats.find(s => s.stat.name === 'attack').base_stat }}</td>
        </tr>
        <tr>
          <th>Defesa:</th>
          <td>{{ pokemon.stats.find(s => s.stat.name === 'defense').base_stat }}</td>
        </tr>
        <tr>
          <th>Ataque Especial:</th>
          <td>{{ pokemon.stats.find(s => s.stat.name === 'special-attack').base_stat }}</td>
        </tr>
        <tr>
          <th>Defesa Especial:</th>
          <td>{{ pokemon.stats.find(s => s.stat.name === 'special-defense').base_stat }}</td>
        </tr>
        <tr>
          <th>Velocidade:</th>
          <td>{{ pokemon.stats.find(s => s.stat.name === 'speed').base_stat }}</td>
        </tr>
      </table>
    </div>
  
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      inputValue: '',
      pokemon: null,
    };
  },
  methods: {
    async searchPokemon() {
      try {
        const { data: pokemon } = await axios.get(`https://pokeapi.co/api/v2/pokemon/${this.inputValue}`);
        this.pokemon = pokemon;
      } catch (error) {
        alert('Pokemon não encontrado, tente novamente!');
      }
    },
  },
};
</script>
