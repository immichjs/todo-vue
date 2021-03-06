<template>
  <div class="todo-list">
    <div class="description-content">
      <i class="far fa-clock"></i>
      <p class="description">{{ todo.description }}</p>
    </div>
    <div class="action">
      <button class="btn-link">Concluído</button>
      <button class="btn-link">Remover</button>
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
    @apply p-3 w-96 rounded-md mt-4;
    background-color: rgba(255, 255, 255, 0.1);
  }

  .description-content, .fa-clock, .action {
    @apply text-gray-300;
  }

  .description-content {
    @apply flex gap-2 items-center text-xl p-2 break-all;
  }

  .action {
    @apply flex justify-end gap-2 p-3 border-gray-800;
  }

  .btn-link {
    @apply p-2 rounded-md cursor-pointer outline-none duration-300;
  }

  .btn-link:hover {
    @apply transform -translate-y-1;
  }

  .btn-link:nth-child(2) {
    @apply text-red-400 duration-300;
  }

  .btn-link:nth-child(2):hover {
    @apply bg-red-400 text-gray-300;
  }
</style>