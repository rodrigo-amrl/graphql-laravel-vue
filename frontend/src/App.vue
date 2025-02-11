<script setup>
import { onMounted, ref } from 'vue';
import { RouterLink, RouterView } from 'vue-router'

const posts = ref([])
onMounted(() =>
  fetch("http://127.0.0.1:8000/graphql", {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      query: `
              query{
                  posts{
                      data{
                          id
                          title
                      }
                  }
              }
    `
    })
  }).then(resp => resp.json())
    .then(result => posts.value = result.data.posts.data)
)
const handleMutation = () => {

}
</script>

<template>
  <ul>
    <li v-for="post in posts" :key="post.id">{{ post.title }}</li>
  </ul>
  <button @click="handleMutation">Mutation</button>
</template>
