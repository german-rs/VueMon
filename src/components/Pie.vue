<script>
import ImagenLogo from './ImagenLogo.vue';
export default{
    components:{ ImagenLogo }
}
</script>
<template>
    <footer class="pie">
        <ImagenLogo class="pie__img" />
        <p>Santiago, 2024.</p>
    </footer>
</template>
<style scoped>
.pie{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1em;
    padding-top: 6em;
    padding-bottom: 2em;
} 
.pie__img{
    width: 100px;
}   
</style>