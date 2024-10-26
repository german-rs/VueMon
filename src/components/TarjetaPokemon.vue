<script>
import EntradaPokemon from './EntradaPokemon.vue';
import BotonDescubrir from './BotonDescubrir.vue';

export default {
  name: 'TarjetaPokemon',
  components: {
    EntradaPokemon,
    BotonDescubrir
  },
  props: {
    pokemon: Object
  },
  data() {
    return {
      adivinanzaUsuario: '',
      esDescubierto: false
    };
  },
  methods: {
    verificarNombre() {
      if (this.adivinanzaUsuario.toLowerCase() === this.pokemon.nombre.toLowerCase()) {
        this.esDescubierto = true;
        this.$emit('descubierto');
      } else {
        alert('Nombre incorrecto, intenta nuevamente');
      }
    }
  }
};
</script>

<template>
    <div class="tarjeta-pokemon">
      <img :src="pokemon.imagen" :class="{ difuminado: !esDescubierto }" alt="pokemon" />
      <div v-if="!esDescubierto">
        <EntradaPokemon v-model="adivinanzaUsuario" @enviarAdivinanza="verificarNombre" />
        <BotonDescubrir @descubrir="verificarNombre" />
      </div>
      <p v-else>{{ pokemon.nombre }}</p>
    </div>
</template>
  
<style scoped>
.tarjeta-pokemon {
  width: 150px;
  margin: 10px;
  text-align: center;
}
img {
  width: 100%;
  height: auto;
  transition: filter 0.3s;
}
.difuminado {
  filter: blur(5px) grayscale(100%);
}
</style>
  