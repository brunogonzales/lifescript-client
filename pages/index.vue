<template>
  <main class="p-4 space-y-2">
    <nuxt-link
      class="text-white py-2 px-2 rounded border-2 border-indigo-400 bg-indigo-400 px-2 py-1 hover:bg-indigo-500"
      to="/create"
      >+ New todo</nuxt-link
    >
    <section v-if="todos.length" class="flex items-center space-x-2 pt-2">
      <select
        v-model="priorityFilter"
        id="priority"
        class="h-10 border border-gray-400 rounded"
      >
        <option disabled value="">Filter by priority</option>
        <option value="low">Low</option>
        <option value="medium">Medium</option>
        <option value="high">High</option>
      </select>
      <client-only
        ><date-picker
          id="duedate"
          placeholder="Filter by due date"
          v-model="dueDateFilter"
          class="pl-1 h-10 items-center justify-center flex border border-gray-400 rounded"
        />
        <span
          @click="
            dueDateFilter = '';
            priorityFilter = '';
          "
          class="text-red-400"
          >Clear</span
        ></client-only
      >
    </section>

    <todos
      :todos="filteredTodos.filter((todo) => !todo.done)"
      todosLabel="Todo"
    />
    <todos
      :todos="filteredTodos.filter((todo) => todo.done)"
      todosLabel="Done"
    />
  </main>
</template>

<script>
export default {
  middleware: "auth",
  async asyncData({ $strapi }) {
    const todos = await $strapi.$todos.find({ "user.id": [$strapi.user.id] });
    return { todos };
  },
  data() {
    return {
      priorityFilter: "",
      dueDateFilter: null,
    };
  },
  computed: {
    filteredTodos() {
      let todos = this.todos;
      if (this.priorityFilter) {
        todos = todos.filter((todo) => todo.priority === this.priorityFilter);
      }
      console.log(todos);

      if (this.dueDateFilter) {
        todos = todos.filter(
          (todo) =>
            this.$dateFns.getTime(this.$dateFns.parseISO(todo.dueDate)) <
            this.$dateFns.getTime(this.dueDateFilter)
        );
      }

      return todos;
    },
  },
};
</script>