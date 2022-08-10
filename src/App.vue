<template>
  <div class="app">
    <my-input
      v-model="searchQuery"
      placeholder="Search..."
    />
     <my-button 
        @click="srtPost"
      >
          search
      </my-button>
    <div class="app__btns">
      <my-button 
        @click="showDialog"
      >
          Create post
      </my-button>
      <my-select
        v-model="selectedSort"
        :options="sortOptions"
      ></my-select>
    </div>
    
      <my-dialog v-model:show="dialogVisible">
        <post-form
          @create="createPost"
        />
      </my-dialog>
      
      <post-list
        :posts="sortedAndSearchedPosts"
        @deletePost="deletePost"
        v-if="!isPostLoading"
      />
      <div v-else>Loading...</div>
      <div class="page__wrapper">
        <div class="page" v-for="page in totalPages" :key="page">
        {{ page }}
        </div>
      </div>
  </div>
</template>

<script>
  import PostList from './components/PostList.vue';
  import PostForm from './components/PostForm.vue';
  import MyDialog from './components/UI/MyDialog.vue';
  import MySelect from './components/UI/MySelect.vue';
  import axios from 'axios';
import MyInput from './components/UI/MyInput.vue';

  export default {
  components: { PostForm, PostList, MyDialog, MySelect, MyInput },
    data() {
      return {
        posts: [],
        dialogVisible: false,
        postLoading: false,
        selectedSort: '',
        searchQuery: '',
        page: 1,
        limit: 10,
        totalPages: 0,
        sortOptions: [
          {
            value: 'title', 
            name: 'By name',
          },
          {
            value: 'body', 
            name: 'By description',
          }
        ]
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
          const res = await axios.get('https://jsonplaceholder.typicode.com/posts?', {
            params: {
              _page: this.page,
              _limit: this.limit,
            }
          });
          this.totalPages = Math.ceil(res.headers['x-total-count'] / this.limit)
          this.posts = res.data
        } catch (error) {
          console.log(error)
        } finally {
          this.isPostLoading = false;
        }
      },
    },

    computed: {
      sortedPosts() {
        return [...this.posts].sort((post1, post2) => {
           post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
        })
      },
 
      sortedAndSearchedPosts() {
        return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
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
    margin: 15px 0;
    display: flex;
    justify-content: space-between;
  }

</style>