<template>
  <div class="flex flex-col">
    <p>{{ label }}</p>
    <input
      :placeholder="placeholder"
      class="border-2 w-full px-1 py-2 rounded border-gray-600"
      :type="isPasswordField ? 'password' : 'text'"
      @input="$emit('input', $event.target.value)"
      :value="value"
    />
  </div>
</template>

<script>
export default {
  // props: ["value", "placeholder", "label"],
  props: {
    value: String,
    placeholder: String,
    label: String,
    isPasswordField: Boolean,
  },
};
</script>

<style>
</style>