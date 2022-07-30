<template>
  <div class="app">
    <div class="app__btns">
      <my-button 
        @click="showDialog"
        style="margin: 15px 0"
      >
          Create post
      </my-button>
      <my-select></my-select>
    </div>
    
      <my-dialog v-model:show="dialogVisible">
        <post-form
          @create="createPost"
        />
      </my-dialog>
      
      <post-list
        :posts="posts"
        @deletePost="deletePost"
        v-if="!isPostLoading"
      />
      <div v-else>Loading...</div>
  </div>
</template>

<script>
  import PostList from './components/PostList.vue';
  import PostForm from './components/PostForm.vue';
  import MyDialog from './components/UI/MyDialog.vue';
  import MySelect from './components/UI/MySelect.vue';
  import axios from 'axios';

  export default {
  components: { PostForm, PostList, MyDialog, MySelect },
    data() {
      return {
        posts: [
          {id: 1, title: 'JavaScript', body: 'Description'}
        ],
        dialogVisible: false,
        postLoading: false,
      }
    },

    mounted() {
      this.fetchPosts()
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
      },

      async fetchPosts() {
        try {
          this.isPostLoading = true;
          const res = await axios.get('https://jsonplaceholder.typicode.com/posts?_liml=10');
          this.posts = res.data
        } catch (error) {
          console.log(error)
        } finally {
          this.isPostLoading = false;
        }
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

  .app__btns {
    padding: 20px 0;
    display: flex;
    justify-content: space-between;
  }

</style>