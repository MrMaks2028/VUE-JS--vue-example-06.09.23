<template>
    <ul>
        <li v-for="item of arr">
            <span v-on:click="onClick(item.id)" v-bind:class="{done: item.done, active: true}">{{ item.title }}</span>
            (<span v-on:click="onDelete(item.id)" class="delete">Удалить</span>)
        </li>
    </ul>
</template>

<script>
export default {
    name: "List",
    props: ["arr"],
    methods: {
        onClick(id) {
            this.$emit('item-done', id);
        },
        onDelete(id) {
            this.$emit('item-remove', id)
        }
    }
}
</script>

<style scoped>

    .done {
        color: #ccc;
        text-decoration: line-through;
    }

    .delete {
        color: red;
        cursor: pointer;
        text-decoration: underline;
    }
</style>