<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title" />
    <button>add</button>
  </form>
</template>

<script>
export default {
  name: 'AddTodo',
  data() {
    return {
      title: ''
    }
  },
  methods: {
    onSubmit() {
      if (this.title.trim()) {
        const td = {
          id: Date.now(),
          title: this.title,
          completed: false
        };
        this.$emit('add-todo', td);

        this.title = '';
      }
    }
  }
}
</script>