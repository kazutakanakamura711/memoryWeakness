<template>
  <div class="message">
    {{ message }}
  </div>
</template>

<script>
export default {
  props: {
    message: String,
  }
}
</script>

<style scoped>
  .message {
  color: aliceblue;
  letter-spacing: 0.4em;
  cursor: pointer;
  transition: 1s;
  font-size: .7em;
  border: solid;
  border-radius: 10px;
  text-align: center;
  margin: 1%;
  padding: 3%;
}

@media screen and (min-width: 481px) {
  .message {
  color: aliceblue;
  letter-spacing: 1.8em;
  cursor: pointer;
  transition: 0.5s;
  font-size: 1em;
  }
}
</style>