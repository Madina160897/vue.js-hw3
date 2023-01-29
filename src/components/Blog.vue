<script>
import List from './List.vue'
export default {
    components: {
        List
    },
    data() {
        return {
            posts: [],
            title: ''
        }
    },
    methods: {
        add() {
            if (this.title === '') {
                return
            }
            const newPost = {
                id: this.posts.length + 1,
                title: this.title,
                comments: [],
            }
            this.posts.push(newPost)
            this.title = ''
        }
    }
}
</script>

<template>
<div class="Post">
    <input type="text" v-model="title" placeholder="type">
    <button class="btn" @click="add">Click</button>
    <List v-for="post in posts" :key="post.id" :posts="post"></List>
</div>
</template>

<style scoped>
.Post {
    display: flex;
    flex-direction: column;
    width: 400px;
    margin: 0 auto;
    border: 2px solid black;
    
}
.btn{
    align-self: flex-end;
    margin-top: 15px;
    margin-bottom: 15px;
}
</style>