<template>
    <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">Projetos</a></li>
        <li><a href="#">Contato</a></li>
        <li v-if="is_online"><a href="#">Meu Perfil</a></li>
    </ul>
</template>

<script>
    export default {
        name: "Header",
        props: ["is_online"]
    }
</script>

<style scoped>
    ul {
        list-style: none;
        display: flex;
        background-color: #999;
        padding: 20px;
        border-radius: 15px;
    }

    li {
        margin-right: 10px;
    }

    a{
        color: #ddd;
        text-decoration: none;
        transition: .5s;
    }

    a:hover {
        color: turquoise;
    }
</style>