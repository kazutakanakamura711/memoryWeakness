<template>
  <div 
    @click="reload" 
    v-show="endFlag"
    :class="{reload:true}"
  ><p>
    {{ nameReload }}
    </p>
  </div>
</template>

<script>
export default {
  props: {
    endFlag: Boolean,
    nameReload: String,
  },
  methods: {
    reload() {
      this.$emit("reload");
    },
  },
};
</script>

<style scoped>
.reload {
  width: fit-content;
  color: aliceblue;
  letter-spacing: 0.4em;
  cursor: pointer;
  transition: 1s;
  font-size: .7em;
  border: solid;
  border-radius: 10px;
  text-align: center;
  margin: 3em auto;
  padding: 1% 2%;
}
.reload:hover {
  color: rgb(243, 247, 10);
}
/* .startBtn {
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
} */

</style>