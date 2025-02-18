<template>
    <div>
        <h1>Create Post</h1>
        <div v-if="error" class="error">{{ error }}</div>
        <div>
            <form action="#" @submit.prevent="createPost">
                <div>
                    <label for="title">Title</label>
                    <input v-model="title" type="text" id="title">
                </div>
                <div>
                    <label for="body">Body</label>
                    <textarea name="body" v-model="body" id="body"></textarea>
                </div>
                <div>
                    <button type="submit">Create</button>
                    <div v-if="loading">Loading...</div>
                </div>
            </form>
        </div>
    </div>

</template>
<script>
import gql from 'graphql-tag';
export default {
    data() {
        return {
            title: "",
            body: "",
            error: null,
            loading: false
        }
    },
    methods: {
        createPost() {
            this.loading = true;
            this.$apollo.mutate({
                mutation: gql`
                mutation createPost($user_id:ID!,$title: String!, $body: String!){
                    createPost(user_id:$user_id,title: $title, body: $body){
                        id
                        title
                        body
                    }
                }
            `,
                variables: {
                    user_id: 1,
                    title: this.title,
                    body: this.body
                }
            })
                .then(data => {
                    console.log(data);
                    this.loading = false
                    this.$router.push('/home');
                })
                .catch(error => {
                    this.error = error.graphQLErrors[0].message
                    this.loading = false
                })
        }
    }
}
</script>
<style>
.error {
    color: red;
    padding: 5px;
}
</style>