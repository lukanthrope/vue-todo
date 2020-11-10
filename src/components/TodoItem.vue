<template>
  <li>
    <span v-bind:class="{completed: todo.completed}">
      {{todo.title}}
      <input type="checkbox" v-on:change="todo.completed = !todo.completed" />
      <button @click="$emit('remove-todo', todo.id)">Delete</button>
    </span>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
</style>