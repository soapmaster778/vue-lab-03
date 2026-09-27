<script setup lang="ts">
import Users from './components/Users.vue'
</script>

<template>
  <main class="app">
    <Users />
  </main>
</template>

<style scoped>
.app {
  display: grid;
  min-height: 100vh;
  padding: 32px;
  place-items: center;
}
</style>
