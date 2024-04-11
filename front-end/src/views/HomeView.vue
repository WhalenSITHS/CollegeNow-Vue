<template>
  <div>
    <div>
      <Signin v-if="!user" />
      <SignUp v-if="user" />
    </div>
    <button @click="change">Already Signed Up?</button>
  </div>
</template>

<script setup>
import { ref } from "vue";
import SignUp from "../components/SignUp.vue";
const username = ref("");
const password = ref("");
const user = true;
function notLogin(username, password) {
  console.log(username);
  console.log(password);
}
function change() {
  user = false;
}
async function login(username, password) {
  try {
    const res = await fetch("http://localhost:3000/login", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        username: username.toLowerCase(),
        password: password,
      }),
    });
    const user = await res.json();
    console.log(user);
  } catch (error) {
    console.log(error);
  }
}
</script>

<style scoped></style>
