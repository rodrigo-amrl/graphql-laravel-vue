<template>

  <nav>
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/about">About</RouterLink>
    <RouterLink to="/posts">Posts</RouterLink>
  </nav>

  <RouterView />
</template>
<script setup>
import { onMounted, ref } from 'vue';
import { RouterLink, RouterView } from 'vue-router'

const posts = ref([])
// onMounted(() =>
//   fetch("http://127.0.0.1:8000/graphql", {
//     method: 'POST',
//     headers: {
//       'Content-Type': 'application/json'
//     },
//     body: JSON.stringify({
//       query: `
//               query{
//                   posts{
//                       data{
//                           id
//                           title
//                       }
//                   }
//               }
//     `
//     })
//   }).then(resp => resp.json())
//     .then(result => posts.value = result.data.posts.data)
// )
const handleMutation = () => {

}
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
