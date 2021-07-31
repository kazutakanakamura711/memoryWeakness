<template>
  <div @click="start" v-show="showStartBtn"
  :class="{startBtn:true}">CLICK<br/>START</div>
</template>

<script>
export default {
  props: {
    showStartBtn: Boolean,
  },
  methods: {
    start() {
      this.$emit("countStart");
    },
  },
};
</script>

<style scoped>
.startBtn {
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
.startBtn:hover {
  color: rgb(243, 247, 10);
}

@media screen and (min-width: 481px) {
  .startBtn {
  color: aliceblue;
  letter-spacing: 1.8em;
  cursor: pointer;
  transition: 0.5s;
  font-size: 1em;
  }
}

</style>