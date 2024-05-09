<template>
  <ul class="size-container">
    <li class="size">Sizes</li>
    <div>
      <li>Large</li>
      <li>Medium</li>
      <li>Small</li>
    </div>
  </ul>
</template>

<script setup></script>

<style scoped>
div {
  display: flex;
  width: 40%;
  justify-content: space-around;
}
.size-container {
  display: flex;
  justify-content: space-between;
  width: 300px;
}
li {
  font-size: 12px;
}
</style>
