<template>
    <div>
        <p>{{ email }}</p>
        <p v-if="is_working">Estou trabalhando no momento.</p>
        <p v-else>Não estou trabalhando no momento</p>        <p v-if="1 > 2">Testando!</p>
        <p>Utilizo as seguintes tecnologias para backend: </p>
        <ul>
            <li v-for="(technology, index) in backend_technologies" :key="index">{{ technology }}</li>
        </ul>
        <p>Utilizo as seguintes tecnologias para frontend:</p>
        <ul>
            <li v-for="technology in frontend_techlogies" :key="technology.id">{{ technology.language }}</li>
        </ul>
        <div>
            <button @click="showEmail">{{ botton_text }}</button>
        </div>
        <p v-show="show_email">Mande uma mensagem para: {{ email }}</p>
        <p class="test">Para acessar meu portifólio basta <a v-bind:href="my_link" target="_blank">clicar aqui</a></p>
        <Picture />
    </div>
</template>

<script>
import Picture from './Picture.vue';

    export default {
        name: 'Info',
        components: {
            Picture
        },
        props: {
            email: String,
            is_working: Boolean,
            my_link: String
        },
        data() {
            return {
                show_email: true,
                botton_text: "Mostrar email",
                backend_technologies: [
                    "JavaScript",
                    "PHP",
                    "Python"
                ],
                frontend_techlogies: [
                    {id: 1, language: "HTML"},
                    {id: 2, language: "CSS"},
                    {id: 3, language: "Vue"}
                ]
            }
        },
        methods: {
            showEmail() {
                this.show_email = !this.show_email
                if(!this.show_email) {
                    this.botton_text = "Mostrar email"
                } else {
                    this.botton_text = "Esconder email"
                }
            }
        }
    }
</script>

<style>
    .paragrafo-pai {
        color: red;
    }
</style>