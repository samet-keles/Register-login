<script setup>
import { computed, ref } from "vue";

import Button from "./components/Buttons/button.vue";
import inputText from "./components/Register/inputText.vue";
import inputEmail from "./components/Register/inputEmail.vue";
import inputPhone from "./components/Register/inputPhone.vue";
import inputPassword from "./components/Register/inputPassword.vue";
import inputConfirm from "./components/Register/inputConfirm.vue";
import inputUsername from "./components/Login/inputUsername.vue";
import loginPassword from "./components/Login/inputPassword.vue";

const show = ref();

const registerInputs = ref({
  fullName: {
    value: "",
    isValid: false,
  },
  email: {
    value: "",
    isValid: false,
  },
  phone: {
    value: "",
    isValid: false,
  },
  password: {
    value: "",
    isValid: false,
  },
  confirm: {
    value: "",
    isValid: false,
  },
});

const loginInputs = ref({
  username: "",
  password: "",
});

const isFormValid = computed(() => {
  const validation = Object.values(registerInputs.value).every(
    (input) => input.isValid
  );

  return validation;
});

const registerHandler = async () => {
  if (!isFormValid.value) return;

  for (const inputName in registerInputs.value) {
    localStorage.setItem(inputName, registerInputs.value[inputName].value);
  }

  return (show.value = show.value == true ? false : true);
};

const loginHandler = async () => {
  const username = localStorage.getItem("email");
  const password = localStorage.getItem("password");

  if (
    username == loginInputs.value.username &&
    password == loginInputs.value.password
  ) {
    return alert("Successful login and registration");
  }

  return alert("Login failed");
};
</script>

<template>
  <div class="card">
    <h1 class="card__title" v-if="!show">Register</h1>
    <form @submit.prevent="registerHandler" v-if="!show">
      <inputText
        v-model:name="registerInputs.fullName.value"
        v-model:validation="registerInputs.fullName.isValid"
        placeholder="Full Name"
      ></inputText>
      <inputEmail
        v-model:email="registerInputs.email.value"
        v-model:validation="registerInputs.email.isValid"
        placeholder="E-mail"
      ></inputEmail>
      <inputPhone
        v-model:phone="registerInputs.phone.value"
        v-model:validation="registerInputs.phone.isValid"
        placeholder="Phone"
      ></inputPhone>
      <inputPassword
        v-model:password="registerInputs.password.value"
        v-model:validation="registerInputs.password.isValid"
        placeholder="Password"
      ></inputPassword>
      <inputConfirm
        :password="registerInputs.password.value"
        v-model:confirm="registerInputs.confirm.value"
        v-model:validation="registerInputs.confirm.isValid"
        placeholder="Confirm Password"
      ></inputConfirm>
      <Button :disabled="!isFormValid" type="submit" name="Register"></Button>
    </form>
    <form @submit.prevent="loginHandler" v-if="show">
      <h1 class="card__title">Login</h1>
      <inputUsername
        v-model:username="loginInputs.username"
        placeholder="Username"
        radius="rounded"
      ></inputUsername>
      <loginPassword
        v-model:password="loginInputs.password"
        placeholder="Password"
        radius="rounded"
      ></loginPassword>
      <Button type="submit" name="Login" color="blue" width="small"></Button>
    </form>
  </div>
</template>

<style lang="scss" scoped>
.card {
  padding: 36px 24px 26px;
  background-color: #ffffff;
  border-radius: 10px;

  &__title {
    font-weight: 700;
    font-size: 44px;
    line-height: 53px;
    margin-bottom: 60px;
    color: #252eff;
  }
}
</style>
