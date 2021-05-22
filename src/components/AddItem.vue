<template>
  <form @submit.prevent="addItem">
    <input type="text" v-model="title">
    <button class="add" type="submit">+</button>
  </form>
</template>

<script>
export default {
  name: "AddItem",
  data() {
    return {title: ''}
  },
  methods: {
    addItem() {

      if (this.title.trim()) {
        const newItem = {
          id: Date.now(),
          title: this.title,
          completed: false

        }
        this.$emit('add', newItem)
        this.title=''
      }
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  justify-content: space-between;
  width: 300px;
}

input {
  padding: 7px 10px;
  width: 250px;
  border-radius: 10px;
}

.add {
  background: green;
  border: none;
  color: white;
  padding: 7px 10px;
  cursor: pointer;
  border-radius: 10px;
}
</style>