<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <header class="flex justify-around">
    <RouterLink to="/">
      <h1>Movie Center</h1>
    </RouterLink>
  </header>

  <main>
    <RouterView />
  </main>
</template>
