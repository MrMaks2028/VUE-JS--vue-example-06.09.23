<template>
    <input type="text" v-model="newItem"/>
    <button v-on:click="add">Добавить</button>
</template>

<script>
export default {
    name: "Form",
    data() {
        return {
            newItem: ''
        }
    },
    methods: {
        add() {
            this.$emit('send-form', this.newItem);
            this.newItem = '';
        }
    }
}
</script>

<style>

</style>