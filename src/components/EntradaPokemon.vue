<script>
export default {
  name: 'EntradaPokemon',
  props: ['valor'],
  data() {
    return {
      valorEntrada: this.valor 
    };
  },
  methods: {
    enviarAdivinanza() {
      this.$emit('enviarAdivinanza', this.valorEntrada);
    }
  },
  watch: {
    valor(nuevoValor) {
      this.valorEntrada = nuevoValor;
    }
  }
}
</script>

<template>
    <input
      v-model="valorEntrada"
      @keyup.enter="enviarAdivinanza"
      placeholder="Escribe el nombre..."
    />
</template>
  
<style scoped>
  input {
    margin-top: 10px;
    padding: 5px;
    width: 100%;
    box-sizing: border-box;
  }
</style>