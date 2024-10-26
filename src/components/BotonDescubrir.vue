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
    padding: 5px;
    width: 100%;
    cursor: pointer;
    }
</style>
  