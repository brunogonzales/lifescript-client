<template>
  <div class="px-4">
    <form class="max-w-md flex flex-col space-y-2" @submit.prevent="saveTodo">
      <text-field
        label="Description"
        placeholder="take out trash"
        v-model="todo.description"
      />
      <div>
        <label for="priority">Priority</label>
        <select v-model="todo.priority" id="priority">
          <option value="low">Low</option>
          <option value="medium">Medium</option>
          <option value="high">High</option>
        </select>
      </div>
      <div>
        <label for="duedate">Due date</label>
        <client-only
          ><date-picker
            id="duedate"
            placeholder="MM/DD/YYYY"
            v-model="todo.dueDate"
        /></client-only>
      </div>
      <div>
        <input type="checkbox" v-model="todo.done" id="done" />
        <label for="done">Mark as done</label>
      </div>
      <button
        class="text-white block w-32 rounded border-2 border-indigo-400 bg-indigo-400 px-2 py-1 hover:bg-indigo-500"
        type="submit"
      >
        Save
      </button>
    </form>
    <button @click="deleteTodo" class="text-red-500 text-center mt-4">
      Delete
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todo: {},
    };
  },
  async mounted() {
    try {
      this.todo = await this.$strapi.$todos.findOne(this.$route.params.id);
    } catch (error) {}
  },

  methods: {
    async saveTodo() {
      try {
        await this.$strapi.$todos.update(this.$route.params.id, {
          ...this.todo,
        });
        this.$router.push("/");
      } catch (error) {}
    },

    async deleteTodo() {
      try {
        await this.$strapi.$todos.delete(this.$route.params.id);
      } catch (error) {}
      this.$router.push("/");
    },
  },
};
</script>

<style>
</style>