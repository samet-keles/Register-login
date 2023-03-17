<script setup>
const props = defineProps(["placeholder", "radius", "password"]);
const emit = defineEmits(["update:password"]);

const passwordHandler = (event) => {
  emit("update:password", event.target.value);
};
</script>

<template>
  <div class="wrapper">
    <input
      class="wrapper__input"
      :class="{ '-rounded': props.radius == 'rounded' }"
      type="password"
      id="l-password"
      name="password"
      :value="password"
      @input="passwordHandler"
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
