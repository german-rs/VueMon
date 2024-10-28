<script>
export default {
  name: 'BotonDescubrir'
}
</script>

<template>
    <button @click="$emit('descubrir')">Descubrir</button>
</template>

<style scoped>
  button {
    margin-top: 5px;
    padding: 8px 5px;
    width: 100%;
    cursor: pointer;
    background-color: var(--color-azul);
    border: none;
    color: var(--color-amarillo);
    border-radius: 8px;
    transition: all .5s ease;
  }
  button:hover{
    box-shadow: 2px 2px 3px var(--color-amarillo);
  }
</style>