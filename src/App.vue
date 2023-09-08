<template>
  <h1>Список Задач</h1>
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
     ],
     lastID: 1,
    }
  },
  methods: {
   onSend(item) {
    const newTask = {id: ++this.lastID, title: item, done: false}
    this.list.unshift(newTask);
    fetch('/api/v1/task', { method: "post", body: JSON.stringify(this.list), headers: {"Content-Type": "application/json"} } );
   },
   onRemove(id) {
    const idx = this.list.findIndex((task) => task.id == id);
    this.list.splice(idx, 1);
   },
   onDone(id) {
    const task = this.list.find((task) => task.id == id);
    task.done = !task.done;
   }
  },
  mounted() {
    fetch('/api/v1/task')
      .then((res) => res.json())
      .then((data) => this.list = data);
  }
}
</script>

<style>

</style>
