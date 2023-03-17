<script setup>
const props = defineProps(["placeholder", "radius", "username"]);
const emit = defineEmits(["update:username"]);

const usernameHandler = (event) => {
  emit("update:username", event.target.value);
};
</script>

<template>
  <div class="wrapper">
    <input
      class="wrapper__input"
      :class="{ '-rounded': props.radius == 'rounded' }"
      type="email"
      id="username"
      name="username"
      :value="username"
      @input="usernameHandler"
      :placeholder="placeholder"
    />
  </div>
</template>

<style lang="scss">
.wrapper {
  &__input {
    &.-rounded {
      border-radius: 20px;
    }
  }
}
</style>
