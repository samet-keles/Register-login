<script setup>
const props = defineProps(["name", "color", "width", "disabled"]);
</script>

<template>
  <button
    class="button"
    :class="{
      '-color': props.color == 'blue',
      '-width': props.width == 'small',
      '-disabled': props.disabled,
    }"
  >
    {{ name }}
  </button>
</template>

<style lang="scss" scoped>
.button {
  width: 352px;
  margin-top: 4rem;
  font-weight: 500;
  font-size: 1.5rem;
  line-height: 1.8rem;
  border-radius: 2rem;

  background-color: #8b54ff;
  color: #ffffff;

  &:hover {
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  }

  &.-color {
    background-color: #252eff;
  }

  &.-width {
    width: 153px;
  }

  &.-disabled {
    pointer-events: none;
    background-color: #8a54ff9f;
    color: #ffffffbb;
  }
}
</style>
