<template>
  <div class="flex py-2">
    <div>
      <p class="text-xl">
        <span>{{ todo.done ? "✅" : "📌" }}</span> {{ todo.description }}
      </p>
      <p v-if="todo.dueDate">
        Due {{ $dateFns.format(todo.dueDate, "dd LLL uuuu") }}
      </p>
      <p
        class="inline uppercase border rounded border-red-300 p-1 text-xs font-bold text-center"
        v-if="todo.priority"
      >
        {{ todo.priority }} priority
      </p>
    </div>
    <nuxt-link :to="'/todo/' + todo.id" class="ml-auto">Edit</nuxt-link>
  </div>
</template>

<script>
export default {
  props: ["todo"],
};
</script>
