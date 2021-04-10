<template>
  <div class="todo-list" :class="{ checked: todo.checked }">
    <div class="description-content">
      <i :class="todo.checked ? 'fas fa-check' : 'fas fa-clock'"></i>
      <p class="description" :class="todo.checked ? 'scratched-line' : ''">{{ todo.description }}</p>
    </div>
    <div class="action">
      <button @click="$emit('toggle', todo)" class="btn-link">
        <span v-if="todo.checked">Desmarcar</span>
        <span v-else>Concluído</span>
      </button>
      <button class="btn-link" @click="$emit('remove', todo)">Remover</button>
    </div>
  </div>
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

<style lang="postcss" scoped>
  .todo-list {
    @apply p-3 mt-4 w-auto rounded-md;
    background-color: rgba(255, 255, 255, 0.1);
    box-shadow: 0 4px 0 rgba(255, 255, 255, 0.05);
  }

  .todo-list:first-child {
    @apply mt-0;
  }

  .description-content, .action {
    @apply text-gray-300 font-medium;
  }

  .description-content {
    @apply flex gap-2 items-center text-xl p-2 break-all;
  }

  .action {
    @apply flex justify-end gap-2 p-3 border-gray-800 flex-wrap;
  }

  .btn-link {
    @apply p-2 rounded-md cursor-pointer outline-none duration-300 font-bold transform lg:hover:translate-y-1;
  }

  .btn-link:nth-child(1) {
    @apply bg-gray-300 text-gray-800;
    box-shadow: 0 3px 0 #A0A3A9;
  }

  .checked {
    @apply bg-green-500;
  }

  .scratched-line {
    @apply line-through text-gray-500;
  }
</style>
