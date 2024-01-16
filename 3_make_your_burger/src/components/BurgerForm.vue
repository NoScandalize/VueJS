<template>
    <div>
        <Message :msg="msg" v-show="msg" />
        <div>
            <form id="burger-form" @submit="createBurger($event)" >
                <div class="input-container">
                    <label for="name">Nome do cliente: </label>
                    <input type="text" name="name" id="name" v-model="name" placeholder="Digite o seu nome">
                </div>
                <div class="input-container">
                    <label for="bread">Escolha o pão: </label>
                    <select name="bread" id="bread" v-model="bread">
                        <option value="">Selecione o seu pão</option>
                        <option v-for="bread in breads" :key="bread.id" :value="bread.tipo">{{ bread.tipo }}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="meat">Escolha a carne do seu Burger: </label>
                    <select name="meat" id="meat" v-model="meat">
                        <option value="">Selecione o tipo de carne</option>
                        <option v-for="meat in meats" :key="meat.id" :value="meat.tipo">{{  meat.tipo  }}</option>
                    </select>
                </div>
                <div id="optionais-container" class="input-container">
                    <label id="opcionais-title" for="optional">Selecione os opcionais: </label>
                    <div v-for="options in optionaldata" :key="options.id" class="checkbox-container">
                        <input type="checkbox" name="optional" v-model="optional" :value="options.tipo">
                        <span>{{ options.tipo }}</span>
                    </div>
                </div>
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar meu Burger">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Message from './Message.vue';

    export default {
        name: 'BurgerForm',
        data() {
            return {
                breads: null,
                meats: null,
                optionaldata: null,
                name: null,
                bread: null,
                meat: null,
                optional: [],
                msg: null
            }
        },components: {
            Message
        },
        methods: {
            async getIngredients() {

                const req = await fetch("http://localhost:3000/ingredientes")
                const { paes, carnes, opcionais } = await req.json();

                this.breads = paes;
                this.meats = carnes;
                this.optionaldata = opcionais;

            },
            async createBurger(e) {

                e.preventDefault();

                const data = {
                    name: this.name,
                    bread: this.bread,
                    meat: this.meat,
                    optional: Array.from(this.optional),
                    status: "Solicitado"
                }

                const dataJSON = JSON.stringify(data);

                const req = await fetch("http://localhost:3000/burgers", {
                    method: "POST",
                    headers: { "Content-Type": "application/json" },
                    body: dataJSON
                });

                const res = await req.json();

                // insert system message
                
                this.msg = "Pedido realizado com sucesso"

                // clean message

                setTimeout(() => this.msg = "", 3000)

                // clean field
                this.name = "";
                this.meat = "";
                this.bread = "";
                this.optional = [];

            }
        },
        mounted() {
            this.getIngredients()
        }
    }
</script>

<style scoped>
    #burger-form {
        max-width: 300px;
        margin: 0 auto;
        margin-bottom: 200px;
    }

    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label {
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #FCBA03;
    }

    input, select {
        padding: 5px 10px;
        width: 300px;
    }

    #optionais-container {
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opcionais-title {
        width: 100%;
    }

    .checkbox-container {
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }

    .checkbox-container span,
    .checkbox-container input {
        width: auto;
    }

    .checkbox-container span {
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn {
        background-color: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: 0.5s;
        border-radius: 10px;
    }

    .submit-btn:hover {
        background-color: #FCBA03;
        color: #222;
        border: 2px solid #222;
    }
</style>