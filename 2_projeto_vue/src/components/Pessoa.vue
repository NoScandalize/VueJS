<template>
    <div>
        <h2>Esta é a descrição da pessoa: {{ name }}</h2>
        <Info :email="email" :is_working=false my_link ="http://google.com/"/>
        <Form />
    </div>
</template>

<script>
import Form from './Form.vue';
import Info from './Info.vue';

    export default {
    name: 'Pessoa',
    data() {
        return {
            name: "Douglas",
            email: "douglas@email.com"
        };
    },
    components: {
    Info,
    Form
}
}
</script>