<template>
    <div id="burger-table">
        <Message :msg="msg" v-show="msg" />
        <div>
            <div id="burger-table-heading">
                <div class="order-id">#</div>
                <div>Cliente</div>
                <div>Pão</div>
                <div>Carne</div>
                <div>Opcionais</div>
                <div>Ações</div>
            </div>
        </div>
        <div id="burger-table-rows">
            <div v-for="(burger, index) in burgers" :key="index" class="burger-table-row">
                <div class="order-number">{{ index + 1 }}</div>
                <div>{{ burger.name }}</div>
                <div>{{ burger.bread }}</div>
                <div>{{ burger.meat }}</div>
                <div>
                    <ul>
                        <li v-for="(opt, index) in burger.optional" :key="index">{{ opt }}</li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status" @change="updateBurger($event, burger.id)">
                        <option value="">Selecione</option>
                        <option v-for="stat in status" :key="stat.id" :value="stat.tipo" :selected="burger.status == stat.tipo">{{ stat.tipo }}</option>
                    </select>
                    <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Message from '../components/Message.vue'

    export default {
        name: 'Dashboard',
        data() {
            return {
                burgers: null,
                burger_id: null,
                status: [],
                msg: null
            }
        },
        components: {
            Message
        },
        methods: {
            async getPedidos() {

                const req = await fetch("http://localhost:3000/burgers");

                const data = await req.json();

                this.burgers = data;

                console.log(this.burgers)

                // get status
                this.getStatus();
                

            },
            async getStatus() {

                const req = await fetch("http://localhost:3000/status")

                const data = await req.json();

                this.status = data;

            },
            async deleteBurger(id) {

                const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                    method: "DELETE"
                })

                const res = await req.json();

                // delete message
                this.msg = "Pedido removido com sucesso"

                setTimeout(() => this.msg = "", 3000)

                // forced update
                this.getPedidos();

            },
            async updateBurger(event, id) {

                const option = event.target.value;

                const dataJson = JSON.stringify({ status: option })

                const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                    method: "PATCH",
                    headers: { "Content-Type": "application/json" },
                    body: dataJson
                })

                const res = await req.json();

                // update message
                this.msg = "Status do pedido atualizado com sucesso"

                setTimeout(() => this.msg = "", 2000)

            }
        },
        mounted() {
            this.getPedidos();
        }
    }
</script>

<style scoped>
    #burger-table {
        max-width: 1200px;
        min-width: 430px;
        margin: 0 auto;
    }

    #burger-table-heading,
    #burger-table-rows,
    .burger-table-row {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
    }

    #burger-table-heading {
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #333;

    }

    #burger-table-heading div,
    .burger-table-row div {
        width: 19%;
    }

    .burger-table-row {
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #ccc;

    }

    #burger-table-heading .order-id,
    .burger-table-row .order-number {
        width: 5%;
    }

    select {
        padding: 12px 5px;
        margin-right: 12px;
        margin-bottom: 10px;
    }

    .delete-btn {
        background-color: #222;
        color: #fcba03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .delete-btn:hover {
        background-color: transparent;
        color: #222;
    }
</style>