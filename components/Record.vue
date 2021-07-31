<template>
  <div>
    TIME　{{ time }}
  </div>
</template>

<script>
export default {
  props: {
    time: null,
  },
};
</script>

<style scoped>
div {
  letter-spacing: 0.4em;
  font-size: .7em;
  color: rgb(93, 252, 191);
}
@media screen and (min-width: 481px) {
  div {
    letter-spacing: 0.8em;
    font-size: 1em;
  }
}
</style>