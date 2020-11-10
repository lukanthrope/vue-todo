<template>
  <div>
    <h1>hellos</h1>
    <ul>
      <TodoItem
        v-for="todo in todos"
        v-bind:todo="todo"
        v-bind:key="todo.id"
        @remove-todo="removeTodo"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from './TodoItem';

export default {
  name: 'TodoList',
  props: ['todos'],
  components: {
    TodoItem,
  },
  methods: {
    removeTodo(id) {
      this.$emit('remove-todo', id);
    }
  }
}
</script>
