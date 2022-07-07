<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'my-button'
}

</script>

<style>
  .btn {
    align-self: flex-end;
    margin-top: 15px;
    padding: 5px 15px;
    color: teal;
    background: white;
  }
</style>