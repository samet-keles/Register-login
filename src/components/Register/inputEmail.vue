<script setup>
import { computed, ref } from "vue";

const isValid = ref();

const props = defineProps(["placeholder", "email", "validation"]);
const emit = defineEmits(["update:email", "update:validation"]);

const emailHandler = (event) => {
  emit("update:email", event.target.value);
  emit("update:validation", isValid.value);
};

isValid.value = computed(() => {
  return /^([\w-]+(?:\.[\w-]+)*)@((?:[\w-]+\.)*\w[\w-]{0,66})\.([a-z]{2,6}(?:\.[a-z]{2})?)$/i.test(
    props.email
  );
});
</script>

<template>
  <div class="wrapper">
    <input
      class="wrapper__input"
      :class="{ '-invalid': !isValid.value }"
      type="email"
      id="email"
      :value="email"
      @input="emailHandler"
      :placeholder="placeholder"
    />
  </div>
</template>
