<template>
  <div class="app">
    <my-button @click="showDialog">Create post</my-button>
      <my-dialog v-model:show="dialogVisible">
        <post-form
          @create="createPost"
        />
      </my-dialog>
      
      <post-list
      :posts="posts"
      @deletePost="deletePost"
      />
  </div>
</template>

<script>
  import PostList from './components/PostList.vue';
  import PostForm from './components/PostForm.vue';
  import MyDialog from './components/UI/MyDialog.vue';

  export default {
  components: { PostForm, PostList, MyDialog },
    data() {
      return {
        posts: [
          {id: 1, title: 'JavaScript', body: 'Description'}
        ],
        dialogVisible: false,
      }
    },

    methods: {
      createPost(post) {
        this.posts.push(post);
        this.dialogVisible = false;
      },

      deletePost(post) {
        this.posts = this.posts.filter(p => p.id !== post.id)
      },

      showDialog() {
        this.dialogVisible = true;
      }
    }
  }

</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .app {
    padding: 15px;
  }

</style>