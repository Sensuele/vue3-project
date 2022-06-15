<template>
  <div class="app">
    <form @submit.prevent>
      <input v-model="title" @input="title = $event.target.value" class="input" type="text" placeholder="Title"/>
      <input v-model="body" @input="body = $event.target.value" class="input" type="text" placeholder="Description"/>
      <button class="btn" @click="createPost">Create</button>
    </form>
    <div>
      <div class="post" v-for="post in posts" :key="post.id">
        <div>
          <strong>Title:</strong>
          {{ post.title }}
        </div>
        <div>
          <strong>Description:</strong>
          {{ post.body }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        title: '',
        body: '',
        posts: [
          {id: 1, title: 'JavaScript', body: 'Description'}
        ]
      }
    },

    methods: {
      createPost() {
        const newPost = {
          id: Date.now(),
          title: this.title,
          body: this.body,
        }

        this.posts.push(newPost);
        this.title = '';
        this.body = '';
      },
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

  .post {
    padding: 15px;
    margin-top: 15px;
    border: 2px solid #ccc;
  }

  .input {
    width: 100%;
    margin-top: 15px;
    padding: 8px 15px;
  }

  form {
    display: flex;
    flex-direction: column;
  }

  .btn {
    align-self: flex-end;
    margin-top: 15px;
    padding: 5px 15px;
    color: teal;
    background: white;
  }
</style>