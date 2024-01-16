<template>
    <div>
        <img :src="avatar" :alt="description">
        <MudarImagem @change-image="changeImg" />
    </div>
</template>

<script>
import MudarImagem from './MudarImagem.vue'

export default {
  components: { MudarImagem },
        name: 'Picture',
        components: {
            MudarImagem
        },
        data() {
            return {
                avatar: "/img/avatar.png",
                description: "Douglas Wesley"
            }
        },
        methods: {
            changeImg() {
                if(this.avatar === "/img/avatar.png") {
                    this.avatar = "/img/avatar2.webp"
                } else {
                    this.avatar = "/img/avatar.png"
                }
            }
        }
    }
</script>