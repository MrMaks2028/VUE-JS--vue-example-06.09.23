<template>
  <div class="wrapper">
    <Form v-on:send-form="onSend"></Form>

    <List v-on:item-done="onDone" v-on:item-remove="onRemove" v-bind:arr="list"></List>
  </div>
</template>

<script>
import List from './components/List.vue';
import Form from './components/Form.vue';

export default {
  name: 'App',
  components: {
    List,
    Form
  },
  data() {
    return {
     list: [
      {id: 1, title: "Завершить проект", done: true}
     ],
     lastID: 1,
    }
  },
  methods: {
   onSend(item) {
    this.list.unshift({id: ++this.lastID, title: item, done: false})
   },
   onRemove(id) {
    const idx = this.list.findIndex((task) => task.id == id);
    this.list.splice(idx, 1);
   },
   onDone(id) {
    const task = this.list.find((task) => task.id == id);
    task.done = !task.done;
   }
  }
}
</script>

<style>

</style>
