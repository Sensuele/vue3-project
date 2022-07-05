<template>
  <form @submit.prevent>
    <input v-model="post.title" class="input" type="text" placeholder="Title" />
    <input v-model="post.body" class="input" type="text" placeholder="Description" />
    <my-button/>
    <button class="btn" @click="createPost">Create</button>
  </form>
</template>

<script>
import MyButton from './UI/MyButton.vue';
  export default {
    components: {MyButton},
    data() {
      return {
        post: {
          title: '',
          body: ''
        }
      }
    },
    methods: {
      createPost() {
        this.post.id = Date.now();
        this.$emit('create', this.post)
        this.post = {
          title: '',
          body: ''
        }
      },
    }
  }
</script>

<style>
  .input {
    width: 100%;
    margin-top: 15px;
    padding: 8px 15px;
  }

  form {
    display: flex;
    flex-direction: column;
  }

</style>