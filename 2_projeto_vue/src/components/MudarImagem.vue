<template>
    <div>
        <button @click="$emit('changeImage')">Trocar imagem de perfil</button>
    </div>    
</template>

<script>
    export default {
        name: "MudarImagem",
        emits: ['changeImage']
    }
</script>