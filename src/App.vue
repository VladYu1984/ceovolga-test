<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
      <nav>
        <RouterLink to="/">Posts</RouterLink>
        <RouterLink to="/post/:id">Article</RouterLink>
      </nav>
  </header>

  <main>
    <RouterView />
  </main>
</template>

<style scoped>
  nav {
    background-color: rgb(249, 236, 140);
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
  }

  main {
    display: flex;
  }
</style>
