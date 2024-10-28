<script>
import axios from 'axios';
import Cabecera from './components/Cabecera.vue';
import TarjetaPokemon from './components/TarjetaPokemon.vue';
import Pie from './components/Pie.vue';

export default {
  components: { 
    Cabecera,
    TarjetaPokemon,
    Pie 
  },
  data() {
    return {
      pokemones: [],
      contadorDescubiertos: 0
    }
  },

  async created() {
    await this.obtenerListaPokemones();
  },
  methods: {
    async obtenerListaPokemones() {
      const url = 'https://pokeapi.co/api/v2/pokemon?limit=20';
      try {
        const respuesta = await axios.get(url);
        this.pokemones = await Promise.all(
          respuesta.data.results.map(pokemon => this.obtenerDetallesPokemon(pokemon))
        );
      } catch (error) {
        console.error("Error al obtener la lista de Pokémon:", error);
      }
    },

    async obtenerDetallesPokemon(pokemon) {
      try {
        const detalles = await axios.get(pokemon.url);
        return {
          nombre: pokemon.name,
          imagen: detalles.data.sprites.front_default
        };
      } catch (error) {
        console.error(`Error al obtener detalles de ${pokemon.name}:`, error);
        return { nombre: pokemon.name, imagen: '' };
      }
    },
    
    aumentarContadorDescubiertos() {
      this.contadorDescubiertos++;
      this.verificarTriunfo();
    },

    verificarTriunfo() {
      if (this.contadorDescubiertos === 20) {
        alert("¡Felicidades! Has descubierto los 20 Pokémones!");
      }
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
}
</script>

<template>
  <div id="app">
    <Cabecera/>
    <p class="contador-texto">Pokémones descubiertos: <span class="contador" >{{ contadorDescubiertos }}/20</span></p>
    <div class="contenedor-pokemones">
      <TarjetaPokemon
        v-for="pokemon in informacionPokemones"
        :key="pokemon.nombre"
        :pokemon="pokemon"
        @descubierto="aumentarContadorDescubiertos"
      />
    </div>
    <Pie/>
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
  gap: 1em;
  max-width: 1000px;
  margin: 0 auto;
}
.contador-texto {
  padding: 1em;
  margin-bottom: 2em;
  font-size: 20px;
  font-weight: 500;
}
.contador {
  font-weight: 700;
  color: #BF9004;
}
</style>