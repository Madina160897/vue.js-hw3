<script>
export default {
    props: {
        posts: {
        type: Object,
        required: true,
        default: {}
        },
        dad: {
            
        }
    },
    data() {
        return{
            title: ''
        }
    },
    methods: {
        addComment() {
            this.posts.comments.push(this.title)
        }
    }
}
</script>


<template>
  <div class="list">
      {{posts.title}}
      <input type="text" v-model="title">
      <button @click="addComment">Save</button>
  </div>
      <div v-for="com in posts.comments" :key="com">
      {{com}}
      </div>
</template>


<style>
.list {
    border: 1px solid teal;
    margin-bottom: 15px;
    display: flex;
    justify-content: space-between;
    padding: 5px;
}
</style>