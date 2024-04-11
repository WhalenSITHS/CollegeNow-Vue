<template>
  <div>
    <div>
      <form name="login-form" @submit.prevent="login(username, password)">
        <div>
          <label for="username">Username: </label>
          <input id="username" type="text" v-model="username" />
        </div>
        <div>
          <label for="password">Password: </label>
          <input id="password" type="password" v-model="password" />
        </div>
        <button class="submit-button" type="submit">Login</button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const username = ref("");
const password = ref("");

function notLogin(username, password) {
  console.log(username);
  console.log(password);
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
