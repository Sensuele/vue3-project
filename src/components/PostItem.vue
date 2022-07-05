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
    <button @click="deletePost">Delete</button>
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