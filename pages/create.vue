<template>
  <main class="px-4 py-2">
    <h2 class="text-xl">New todo</h2>
    <form class="max-w-md flex flex-col space-y-2" @submit.prevent="submit">
      <text-field
        label="Description"
        placeholder="take out trash"
        v-model="description"
      />
      <div>
        <label for="priority">Priority</label>
        <select v-model="priority" id="priority">
          <option disabled value="">Select</option>
          <option value="low">Low</option>
          <option value="medium">Medium</option>
          <option value="high">High</option>
        </select>
      </div>
      <div>
        <label for="duedate">Due date</label>
        <client-only
          ><date-picker id="duedate" placeholder="MM/DD/YYYY" v-model="dueDate"
        /></client-only>
      </div>
      <div>
        <input type="checkbox" v-model="done" id="done" />
        <label for="done">Mark as done</label>
      </div>
      <button
        class="text-white block w-32 rounded border-2 border-indigo-400 bg-indigo-400 px-2 py-1 hover:bg-indigo-500"
        type="submit"
      >
        Save
      </button>
    </form>
  </main>
</template>

<script>
export default {
  data() {
    return {
      description: "",
      done: false,
      dueDate: null,
      priority: null,
    };
  },
  methods: {
    async submit() {
      try {
        await this.$strapi.$todos.create({
          description: this.description,
          done: this.done,
          dueDate: this.dueDate,
          priority: this.priority,
          user: this.$strapi.user,
        });
        this.$router.push("/");
      } catch (e) {}
    },
  },
};
</script>

<style>
</style>