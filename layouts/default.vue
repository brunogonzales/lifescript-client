<template>
  <div class="max-w-md mx-auto">
    <div v-if="$strapi.user" class="flex px-4 pt-2">
      <nuxt-link class="font-bold" to="/">{{
        $strapi.user.username
      }}</nuxt-link>
      <p class="ml-auto cursor-pointer" @click="logout">Logout</p>
    </div>
    <Nuxt />
  </div>
</template>

<script>
export default {
  methods: {
    logout() {
      this.$strapi.logout();
      this.$router.push("/login");
    },
  },
};
</script>