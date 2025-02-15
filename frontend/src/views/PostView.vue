<template>
    <div>

        <h1>Post page for id: {{ $route.params.id }}</h1>
        <div v-if="$apollo.queries.post.loading">
            Loading....
        </div>
        <div v-else>
            <h1>{{ post.title }}</h1>
            <p>{{ post.body }}</p>
        </div>
    </div>

</template>
<script>
import gql from 'graphql-tag'

export default {
    data() {
        return {
            post: []
        }
    },
    apollo: {
        post: {
            query: gql`
                query Post($id: ID!) {
                    post(id: $id) {
                        id
                        title
                        body
                    }
                }
            `,
            variables() {
                return {
                    id: this.$route.params.id
                }
            }
        }
    }

}
</script>