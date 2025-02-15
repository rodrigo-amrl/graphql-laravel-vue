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