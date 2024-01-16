<template>
    <footer id="footer">
        <p>Make Your Burger &copy; 2024</p>
    </footer>
</template>

<script>
    export default {
        name: 'Footer',
    }
</script>

<style scoped>
    #footer {
        height: 150px;
        background-color: #272727;
        border-top: 2px solid #2b2b2b;
        box-shadow: 1px -5px 10px #111111b0;
        font-family: Arial, Helvetica, sans-serif;
        font-weight: bold;
        color: #FCBA03;
        position: fixed;
        bottom: 0;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;
    }
</style>