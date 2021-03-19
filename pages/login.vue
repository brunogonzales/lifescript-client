<template>
  <div class="p-4 space-y-2">
    <h2 class="text-center text-xl">Login</h2>
    <form class="mx-auto space-y-2" @submit.prevent="login">
      <text-field
        v-model="username"
        label="Username"
        placeholder="lovefrog123"
      />
      <text-field
        v-model="password"
        label="Password"
        placeholder="******"
        isPasswordField
      />
      <button
        class="text-white rounded border-2 border-indigo-400 bg-indigo-400 px-2 py-4 w-full mt-2 hover:bg-indigo-500"
        type="submit"
      >
        Login
      </button>
    </form>
    <p class="text-center">
      Don't have an account yet?
      <nuxt-link class="text-indigo-700" to="/register">Register</nuxt-link>
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    async login() {
      try {
        await this.$strapi.login({
          identifier: this.username,
          password: this.password,
        });
        this.$router.push("/");
      } catch (e) {}
    },
  },
};
</script>

<style>
</style>