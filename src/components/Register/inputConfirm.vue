<script setup>
import { computed, ref } from "vue";

const isValid = ref();

const props = defineProps(["placeholder", "confirm", "password", "validation"]);
const emit = defineEmits(["update:confirm", "update:validation"]);

const confirmHandler = (event) => {
  emit("update:confirm", event.target.value);
  emit("update:validation", isValid.value);
};

isValid.value = computed(() => {
  return props.confirm == props.password;
});
</script>

<template>
  <div class="wrapper">
    <input
      class="wrapper__input"
      :class="{ '-invalid': !isValid.value }"
      type="password"
      id="confirm"
      :value="confirm"
      @input="confirmHandler"
      :placeholder="placeholder"
    />
  </div>
</template>
