<template>
  <p>{{ name }}</p>
</template>

<script>
export default {
  props: {
    name: String,
  }
}
</script>

<style scoped>
  p {
    text-align: center;
    letter-spacing: 1em;
    font-size: .7em;
    color: rgb(93, 252, 191);
  }
</style>