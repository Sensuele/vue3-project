<template>
  <div v-if="posts.length > 0">
    <h3>Posts</h3>
    <transition-group name="user-list">
      <post-item
        v-for="post in posts"
        :key="post.id"
        :post="post"
        @deletePost="$emit('deletePost', post)"
      />
    </transition-group>
    
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

  .user-list-item {
    display: inline-block;
    margin-right: 10px;
  }
  .user-list-enter-active,
  .user-list-leave-active {
    transition: all .4s ease;
  }
  .user-list-enter-from,
  .user-list-leave-to {
    opacity: 0;
    transform: translateX(30px);
  }

  .user-list-move {
    transition: transform 0.4s ease;
  }
</style>