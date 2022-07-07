<template>
  <form @submit.prevent>
    <my-input v-model="post.title" placeholder="Title" />
    <my-input v-model="post.body" placeholder="Description" />
    <my-button @click="createPost">Create</my-button>
  </form>
</template>

<script>
  export default {
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
  form {
    display: flex;
    flex-direction: column;
  }

</style>