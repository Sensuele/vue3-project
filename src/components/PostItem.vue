<template>
  <div class="post">
    <div>
      <strong>Title:</strong>
      {{ post.title }}
    </div>
    <div>
      <strong>Description:</strong>
      {{ post.body }}
    </div>
    <my-button @click="deletePost">Delete</my-button>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    }
  },

  methods: {
    deletePost(event) {
      console.log(event.target)
    }
  }
}
</script>

<style>

</style>