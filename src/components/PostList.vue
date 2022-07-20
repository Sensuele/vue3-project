<template>
  <div v-if="posts.length > 0">
    <h3>Posts</h3>
      <post-item
      v-for="post in posts"
      :key="post.id"
      :post="post"
      @deletePost="$emit('deletePost', post)"
      />
  </div>
 <h2 v-else>
  Empty list
 </h2>
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
    },

  }
</script>

<style scoped>
  .post {
    padding: 15px;
    margin-top: 15px;
    border: 2px solid #ccc;
  }
</style>