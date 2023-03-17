<script setup>
import { computed, ref } from "vue";

const show = ref();
const isValid = ref();
const providedItems = ref({
  charLength: false,
  upperLetter: false,
  lowerLetter: false,
  number: false,
  specialChar: false,
});

const props = defineProps(["placeholder", "password", "validation"]);
const emit = defineEmits(["update:password", "update:validation"]);

const passwordHandler = (event) => {
  emit("update:password", event.target.value);
  emit("update:validation", isValid.value);
};

const showHandler = () => {
  return (show.value = true);
};

providedItems.value = {
  charLength: computed(() => {
    return props.password.length >= 8 && props.password.length <= 16;
  }),
  upperLetter: computed(() => {
    return /[A-Z]+/.test(props.password);
  }),
  lowerLetter: computed(() => {
    return /[a-z]+/.test(props.password);
  }),
  number: computed(() => {
    return /[0-9]+/.test(props.password);
  }),
  specialChar: computed(() => {
    return /\W+/.test(props.password);
  }),
};

isValid.value = computed(() => {
  const validation = Object.values(providedItems.value).every((item) => item);
  if (validation) show.value = false;
  return validation;
});
</script>

<template>
  <div class="wrapper">
    <input
      class="wrapper__input"
      :class="{ '-invalid': !isValid.value }"
      type="password"
      id="password"
      :value="password"
      @input="passwordHandler"
      @click="showHandler"
      :placeholder="placeholder"
    />
    <Transition>
      <p class="wrapper__info" v-show="show">
        <span :class="{ '-provided': providedItems.charLength }">
          Minimum eight characters,</span
        >
        <span :class="{ '-provided': providedItems.upperLetter }"
          >at least one uppercase letter,</span
        >
        <span :class="{ '-provided': providedItems.lowerLetter }"
          >one lowercase letter,</span
        >
        <span :class="{ '-provided': providedItems.number }">one number</span>
        <span :class="{ '-provided': providedItems.specialChar }"
          >and one special character</span
        >
      </p>
    </Transition>
  </div>
</template>

<style lang="scss" scoped>
.wrapper {
  .v-enter-active,
  .v-leave-active {
    transition: opacity 0.7s ease;
  }

  .v-enter-from,
  .v-leave-to {
    opacity: 0;
  }

  &__info {
    display: flex;
    justify-content: space-evenly;
    flex-wrap: wrap;
    max-width: 350px;
    font-size: 1.1rem;
    color: #ff1111;

    .-provided {
      color: #6066ff;
    }
  }
}
</style>
