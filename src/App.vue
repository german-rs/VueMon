<script>
import axios from 'axios';
import Cabecera from './components/Cabecera.vue';
import TarjetaPokemon from './components/TarjetaPokemon.vue';

export default {
  components: { 
    Cabecera,
    TarjetaPokemon 
  },
  data() {
    return {
      pokemones: [],
      contadorDescubiertos: 0
    };
  },
  async created() {
    await this.cargarPokemones();
  },
  methods: {
    // Mejorar esta función, muy sobrecargada.
    async cargarPokemones() {
      const url = 'https://pokeapi.co/api/v2/pokemon?limit=20';
      try {
        const respuesta = await axios.get(url);
        this.pokemones = await Promise.all(respuesta.data.results.map(async (pokemon) => {
          const detalles = await axios.get(pokemon.url);
          return {
            nombre: pokemon.name,
            imagen: detalles.data.sprites.front_default
          };
        }));
      } catch (error) {
        console.error("Error al obtener datos de Pokémon:", error);
      }
    },
    incrementarContadorDescubiertos() {
      this.contadorDescubiertos++;
    }
  },
  computed: {
    informacionPokemones() {
      return this.pokemones.map(pokemon => ({
        nombre: pokemon.nombre,
        imagen: pokemon.imagen
      }));
    }
  }
};
</script>

<template>
  <div id="app">
    <Cabecera/>
    <p>Pokémones descubiertos: {{ contadorDescubiertos }}/20</p>
    <div class="contenedor-pokemones">
      <TarjetaPokemon
        v-for="pokemon in informacionPokemones"
        :key="pokemon.nombre"
        :pokemon="pokemon"
        @descubierto="incrementarContadorDescubiertos"
      />
    </div>
  </div>
</template>

<style>
#app {
  text-align: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
.contenedor-pokemones {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
