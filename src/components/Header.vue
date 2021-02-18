<template>
    <header class="user-container">
      <form @submit.prevent="addTodo(todo)">
        <input type="text" class="todo-text" placeholder="Novo todo" v-model="todo.description">
        <button class="add-todo">Adicionar</button>
      </form>
    </header>
</template>

<script>
export default {
    data() {
    return {
      todos: [],
      todo: {
        checked: false
      }
    }
  },

  methods: {
    addTodo(todo) {
      todo.id = Date.now()
      
      this.todos.push(todo)
      this.todo = { checked: false }
    }
  },
}
</script>

<style lang="postcss" scoped>
  .user-container {
    @apply flex w-full box-border justify-center;
  }

  .user-container form {
    @apply flex w-96;
  }

  .todo-text, .add-todo {
    @apply p-3 outline-none rounded-md font-medium;
  }

  .todo-text {
    @apply text-gray-300 font-medium w-full mr-1.5;
    background-color: rgba(255, 255, 255, 0.1);
  }

  .add-todo {
    @apply bg-gray-300 text-gray-800;
  }
</style>