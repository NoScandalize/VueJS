<template>
    <div>
        <button @click="first(txt1, $event), second(txt2, $event), third(txt3, $event)">Ativar múltiplos eventos</button>
        <p>{{ multi_event }}</p>
    </div>
</template>

<script>
    export default {
        name: "MultiplosEventos",
        data() {
            return {
                multi_event: "",
                txt1: "Primeiro evento",
                txt2: "Segundo evento",
                txt3: "Terceiro evento"
            }
        },
        methods: {
            first(txt) {
                this.multi_event = txt;
            },
            second(txt) {
                setTimeout(() => this.multi_event = txt, 1000)
            },
            third(txt) {
                setTimeout(() => this.multi_event = txt, 2000)
            }
        }
    }
</script>

<style scoped>
    div {
        margin: 100px;
    }
</style>