<script>
import ImagenLogo from './ImagenLogo.vue';
export default{
    components:{ ImagenLogo }
}
</script>

<template>
    <header class="cabecera">
       <ImagenLogo class="cabecera__img" /> 
       <h1>¿Quién es ese Pokémon?</h1>
    </header>
</template>

<style scoped>
.cabecera{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 1em;
    gap: 2em;
    margin-bottom: 1em;
}

.cabecera__img{
    width: 300px;
}

@media (min-width: 475px){
    .cabecera__img{
        width: 350px;
    }
}

@media (min-width: 640px){
    .cabecera__img{
        width: 400px;
    }
}

@media (min-width: 768px){
    .cabecera__img{
        width: 450px;
    }
}

@media (min-width: 1024px){
    .cabecera__img{
        width: 500px;
    }
}
</style>