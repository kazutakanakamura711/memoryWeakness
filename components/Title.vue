<template>
  <h1>{{ title }}</h1>
</template>

<script>
export default {
  props: {
    title: String,
  }
}
</script>

<style>
  h1 {
    letter-spacing: 0.6em;
    font-size: 4em;
    margin: 100px auto ;
    text-align: center;
    color: aliceblue;
  }
</style>