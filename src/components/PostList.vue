<template>
  <div>
    <h3>Users</h3>
      <post-item
      v-for="post in posts"
      :key="post.id"
      :post="post"
      />
  </div>
 
</template>

<script>
import PostItem from './PostItem.vue'
  export default {
  components: { PostItem },
    props: { 
      posts: { 
        type: Array,
        required: true,
      }
    }
  }
</script>

<style scoped>
  .post {
    padding: 15px;
    margin-top: 15px;
    border: 2px solid #ccc;
  }
</style>