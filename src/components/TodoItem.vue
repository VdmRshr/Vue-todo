<template>
  <li>
    <span v-bind:class="{done:item.completed===true}">
      <input type="checkbox"
             v-on:change="item.completed=!item.completed">
      <strong>{{index+1}} {{ item.title | uppercase}}</strong>
    </span>
    <button class="rm"
            v-on:click="$emit('remove-item',item.id)">
      &times;
    </button>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    item: {
      type: Object,
      required: true
    },
    index:Number
  },
  filters:{
    uppercase(value){
      return value.toUpperCase()
    }
  }
}
</script>

<style scoped>
li {
  border-bottom: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: 15px;
}

.rm {
  background: red;
  border: none;
  color: white;
  padding: 7px 10px;
  cursor: pointer;
  border-radius: 10px;
}

.done {
  text-decoration: line-through;
}

</style>