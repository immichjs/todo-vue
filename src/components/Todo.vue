<template>
  <div>
    <header class="user-container">
      <form @submit.prevent="addTodo(todo)">
        <input type="text" class="todo-text" placeholder="Novo todo" v-model="todo.description">
        <button class="add-todo">Adicionar</button>
      </form>
    </header>
    <main class="todo-container">
        <div v-for="t in todos" :key="t.id">
          <div class="todo-list">
            <div class="description-content">
              <p class="description">{{ t.description }}</p>
            </div>
            <div class="action">
              <button class="btn-link">Concluído</button>
              <button class="btn-link">Remover</button>
            </div>
        </div>
      </div>
    </main>
  </div>
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
  }
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

  .description-content {
    @apply flex items-center justify-center text-xl mb-1 p-2;
  }

  .action {
    @apply flex justify-end gap-2 p-3 border-b-2 border-gray-800;
  }

  .btn-link {
    @apply p-2 rounded-md cursor-pointer outline-none;
  }
  
  .btn-link:nth-child(n+2) {
    @apply text-red-400;
  }

  .add-todo {
    @apply bg-gray-300 text-gray-800;
  }
  
  .todo-container {
    @apply flex justify-center w-96 my-3;
  }

  .todo-list {
    @apply p-3 w-96 rounded-md;
    background-color: rgba(255, 255, 255, 0.1);
  }

  .description-content, .title-content, .action {
    @apply text-gray-300;
  }
</style>