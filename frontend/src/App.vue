<template>

  <nav>
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/about">About</RouterLink>
    <RouterLink to="/post/create">Create</RouterLink>
  </nav>

  <RouterView />
</template>
<script setup>
import { RouterLink, RouterView } from 'vue-router'

</script>
<style>
nav {
  background-color: #333;
  padding: 10px;
  display: flex;
  gap: 15px;
}

nav a {
  color: white;
  text-decoration: none;
  font-size: 18px;
  padding: 8px 12px;
  border-radius: 5px;
  transition: background 0.3s;
}

nav a:hover {
  background-color: #555;
}

nav a.router-link-exact-active {
  background-color: #555;
}
</style>
