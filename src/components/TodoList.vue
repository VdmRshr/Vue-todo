<template>
  <div>
    <ul>
      <TodoItem
          v-for="(item,i) of todos"
          v-bind:item="item" :key="item.id"
          v-bind:index="i"
          v-on:remove-item="removeItem"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from "@/components/TodoItem";

export default {
  name: "TodoList",
  props: ['todos'],
  components: {
    TodoItem
  },
  methods: {
    removeItem(id) {
      console.log(id)
      this.$emit('remove-item', id)
    }
  }
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>