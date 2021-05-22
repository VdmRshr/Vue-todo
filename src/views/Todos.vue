<template>
  <div>
    <h2>Todo App</h2>
    <hr>
    <router-link to="/">Home</router-link>

    <hr>
    <AddItem
        @add="addItem"
    />
    <select v-model="filter">
      <option value="all">All</option>
      ion
      <option value="completed">Completed</option>
      ion
      <option value="not-completed">Not completed</option>
      ion
    </select>
    <hr>
    <Loader v-if="loading"/>
    <TodoList
        v-else-if="filteredItems.length"
        v-bind:todos="filteredItems"
        @remove-item="removeItem"
    />
    <p v-else> No items</p>
  </div>
</template>

<script>

import TodoList from '@/components/TodoList';
import AddItem from "@/components/AddItem";
import Loader from "@/components/Loader";

export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  components: {
    AddItem,
    TodoList,
    Loader
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
        .then(response => response.json())
        .then(json => {
          this.todos = json
          this.loading = false
        })
  },
  // watch: {
  //   filter(value) {
  //
  //   }
  // }
  computed:{
    filteredItems(){
      if(this.filter==='all') return this.todos
      if(this.filter==='completed') return this.todos.filter(i=>i.completed)
      if(this.filter==='not-completed') return this.todos.filter(i=>!i.completed)
    return null
    }
  },
  methods: {
    removeItem(id) {
      this.todos = this.todos.filter(i => i.id !== id)
    },
    addItem(item) {
      this.todos.push(item)
    }
  }
}
</script>

<style scoped>

</style>