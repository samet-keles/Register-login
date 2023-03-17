<script setup>
import { computed, ref } from "vue";

const isValid = ref();

const props = defineProps(["placeholder", "phone", "validation"]);
const emit = defineEmits(["update:phone", "update:validation"]);

const phoneHandler = (event) => {
  emit("update:phone", event.target.value);
  emit("update:validation", isValid.value);
};

isValid.value = computed(() => {
  return /^([(]?[+]{1}[0-9]{1,3}[)]?[ .\-]?)?[(]?[0-9]{3}[)]?[ .\-]?([0-9]{3}[ .\-]?[0-9]{4}|[a-zA-Z0-9]{7})([ .\-]?[/]{1}[ .\-]?[0-9]{2,4})?$/.test(
    props.phone
  );
});
</script>

<template>
  <div class="wrapper">
    <input
      class="wrapper__input"
      :class="{ '-invalid': !isValid.value }"
      type="tel"
      id="phone"
      :value="phone"
      @input="phoneHandler"
      :placeholder="placeholder"
    />
  </div>
</template>
