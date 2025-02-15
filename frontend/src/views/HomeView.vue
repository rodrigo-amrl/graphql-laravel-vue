<template>
  <div>
    <div v-if="$apollo.queries.posts.loading">Loading...</div>
    <ul v-else>
      <li v-for="post in posts" :key="post.id">
        <router-link :to="{ name: 'post', params: { id: post.id } }">View
          {{ post.title }}

        </router-link>
      </li>
    </ul>
    <div>
      <h2>Apolo Query Component</h2>
      <ApolloQuery :query="gql => gql`
          query getPosts {
            posts {
              data {
                id
                title
              }
            }
          }
        `" :variables="{ first: 5 }">
        <template v-slot="{ result: { loading, error, data } }">
          <div v-if="loading">Loading...</div>
          <div v-else-if="error">Error: {{ error.message }}</div>
          <div v-else-if="data">
            <ul>
              <li v-for="post in data.posts.data" :key="post.id">
                <router-link :to="{ name: 'post', params: { id: post.id } }">View
                  {{ post.title }}

                </router-link>
              </li>
            </ul>
          </div>
          <div v-else>Nothing</div>
        </template>
      </ApolloQuery>
    </div>
  </div>

</template>
<script>
import gql from 'graphql-tag'

export default {
  data() {
    return {
      posts: []
    }
  },
  apollo: {
    posts: {
      query: gql`
      query{
          posts{
              data{
                  id
                  title
              }
          }
      }`,
      update(data) {
        return data.posts.data
      }
    }
  }
}
</script>