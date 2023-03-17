<script setup>
import { computed, ref } from "vue";

const isValid = ref();

const props = defineProps(["placeholder", "name", "validation"]);
const emit = defineEmits(["update:name", "update:validation"]);

const nameHandler = (event) => {
  emit("update:name", event.target.value);
  emit("update:validation", isValid.value);
};

isValid.value = computed(() => {
  return /^[a-zA-ZÃ§Ã‡Ä±ÄŸÄžÄ°Ã¶Ã–ÅŸÅžÃ¼Ãœ]+(?:\s[a-zA-ZÃ§Ã‡Ä±ÄŸÄžÄ°Ã¶Ã–ÅŸÅžÃ¼Ãœ]+)+$/.test(
    props.name
  );
});
</script>

<template>
  <div class="wrapper">
    <input
      class="wrapper__input"
      :class="{ '-invalid': !isValid.value }"
      type="text"
      id="name"
      name="name"
      :value="name"
      @input="nameHandler"
      :placeholder="placeholder"
    />
  </div>
</template>
<style lang="scss">
.wrapper {
  margin-bottom: 2rem;

  &__input {
    width: 352px;
    padding: 1rem;
    font-size: 15px;
    line-height: 18px;
    border: 2px solid #6066ff;
    border-radius: 10px;

    background-color: #fff;
    color: rgba(0, 0, 0, 0.9);

    &:hover {
      filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    }

    &:focus-visible {
      outline: #6066ff;
      filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    }

    &::placeholder {
      color: rgba(0, 0, 0, 0.7);
    }

    &.-invalid:focus-visible {
      border-color: #ff6060;
    }
  }
}
</style>
