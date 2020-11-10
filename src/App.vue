<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <AddTodo @add-todo="addTodo" />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not-Completed</option>
    </select>
    <Loader v-if="isLoading" />
    <TodoList v-else-if="filteredTodos.length" v-bind:todos="filteredTodos" @remove-todo="deleteTodo" />
    <p v-else>No todos</p>
  </div>
</template>

<script>

import TodoList from './components/Todolist';
import AddTodo from './components/AddTodo';
import Loader from './components/Loader';

export default {
  name: 'App',
  data() {
    return {
      todos: [],
      isLoading: true,
      filter: 'all'
    }
  },
  computed: {
    filteredTodos() {
      if (this.filter === 'all') return this.todos;
      if (this.filter === 'completed') return this.todos.filter(el => el.completed);
      return this.todos.filter(el => !el.completed);
    }
  },
  async mounted() {
    this.isLoading = true;
    const res = await fetch('https://jsonplaceholder.typicode.com/todos?_limit=5');
    const data = await res.json();

    this.todos = data;
    this.isLoading = false;
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(el => el.id !== id);
    },
    addTodo(td) {
      this.todos.push(td);
    }
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
