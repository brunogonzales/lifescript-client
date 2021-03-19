<template>
  <section
    v-if="todos.length"
    class="flex flex-col space-y-2 pt-2 divide-y divide-gray-500"
  >
    <h2 class="font-bold">{{ todosLabel }}</h2>
    <todo v-for="todo in todos" :todo="todo" :key="todo.id" />
  </section>
</template>

<script>
export default {
  props: ["todos", "todosLabel"],
};
</script>

<style>
</style>