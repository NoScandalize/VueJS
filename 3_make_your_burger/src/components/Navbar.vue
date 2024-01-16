<template>
    <nav id="nav">
        <router-link to="/" id="logo-url">
            <img :src="logo" :alt="alt" id="logo">
        </router-link>
        <router-link to="/" class="btn-nav">Home</router-link>
        <router-link to="/pedidos" class="btn-nav">Pedidos</router-link>
    </nav>
</template>

<script>
    export default {
        name: "Navbar",
        props: ["logo", "alt"]
    }
</script>

<style scoped>
    #nav {
        background-color: #272727;
        border: 2px solid #2b2b2b;
        box-shadow: 1px 5px 10px #111111b0;
        padding: 15px 50px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
        position: fixed;
        top: 0;
        width: 100%;
    }

    #nav #logo-url {
        margin: auto;
        margin-left: 0;
    }

    #logo {
        width: 40px;
        height: 40px;
        transition: .5s;
    }

    #logo:hover {
        transform: scale(1.2);
    }

    #nav a {
        color: #000;
        text-decoration: none;
        margin: 12px;
        transition: .5s;
        font-weight: bold;
        font-family: Arial, Helvetica, sans-serif;
    }

    #nav a:hover {
        color: #FCBA03;
    }

    .btn-nav {
        padding: 8px 16px;
        background-color: #FCBA03;
        border-radius: 8px;
        border: 1px solid #000;
        box-shadow: 2px 5px 10px #111111b0;
    }

    .btn-nav:hover {
        background-color: #222;
        border: 1px solid #FCBA03;
    }
</style>