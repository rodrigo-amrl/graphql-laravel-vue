<template>
    <div>
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
        <ApolloQuery :query="gql => gql`
                query Post($id: ID!) {
                    post(id: $id) {
                        id
                        title
                        body
                    }
                }
            `" :variables="{ id: $route.params.id }">
            <template v-slot="{ result: { data, loading } }">
                <div v-if="loading">
                    Loading....
                </div>
                <div v-else>
                    <h1>{{ data.post.title }}</h1>
                    <p>{{ data.post.body }}</p>
                </div>
            </template>
        </ApolloQuery>
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