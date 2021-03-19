<template>
  <div class="p-4 space-y-2">
    <h2 class="text-center text-xl">Register</h2>
    <form class="max-w-md mx-auto space-y-2" @submit.prevent="register">
      <text-field
        v-model="username"
        label="Username"
        placeholder="lovefrog123"
      />
      <text-field v-model="email" label="Email" placeholder="frog@mail.com" />
      <text-field
        v-model="password"
        label="Password"
        placeholder="******"
        isPasswordField
      />
      <button
        class="text-white rounded border-2 border-pink-400 bg-pink-400 px-2 py-4 w-full mt-2 hover:bg-pink-500"
        type="submit"
      >
        Register
      </button>
    </form>
    <p class="text-center">
      Already have an account?
      <nuxt-link class="text-pink-700" to="/login">Login</nuxt-link>
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      password: "",
      email: "",
    };
  },
  methods: {
    async register() {
      try {
        await this.$strapi.register({
          email: this.email,
          username: this.username,
          password: this.password,
        });
        this.$router.push("/");
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>

<style>
</style>