<template>
  <div>
      <ul>
        <li v-for="(card, i) in cardsArr" :key="i"
        :class="{open:card.isOpen, del:card.isDel}"
        @click="open(i)">
          <div class="mark">
            <div v-show="card.isOpen" :class="{black:card.isBlack, red:card.isRed}">{{ card.mark }}</div>
          </div>
          <div class="num">
            <div v-show="card.isOpen">{{ card.num }}</div>
          </div>
        </li>
      </ul>
  </div>
</template>

<script>
export default {
  props: {
    cardsArr: Array,
  },
  methods: {
    open(i) {
      this.$emit('open',i)
    }
  }
}
</script>

<style scoped>
body{
  min-width: 128px;
  height: auto;
}
ul {
  width: 100%;
  height: auto;
  display: flex;
  flex-wrap: wrap; /* 折返し指定 */
  justify-content: center;
  align-items: center;
  padding: 0;
}
.open {
  color: black;
  background: white;
}

li {
  background-image: url('/images/nuxtColor.png');
  background-size: contain;
  user-select: none;
  color: rgb(190, 12, 12);
  font-size: 1.3rem;
  line-height: 92px;
  width: 2rem;
  height: 2.82rem;
  /* background: rgb(190, 12, 12); */
  border: solid #aaa;
  border-radius: 5px;
  list-style: none;
  margin: 0.6rem;
  cursor: pointer;
}

.mark {
  font-size: 0.8rem;
  line-height: 16px;
}
.num {
  line-height: 20px;
  text-align: center;
}
.del {
  visibility: hidden;
}
.black {
  color: black;
}
.red {
  color: rgb(190, 12, 12);
}

@media screen and (min-width: 481px) {
	/* 481px以上に適用されるCSS（タブレット用） */
  li {
    background-image: url('/images/nuxtColor.png');
    background-size: contain;
    user-select: none;
    color: rgb(190, 12, 12);
    font-size: 2rem;
    line-height: 92px;
    width: 4rem;
    height: 6.3rem;
    /* background: rgb(190, 12, 12); */
    border: solid #aaa;
    border-radius: 5px;
    list-style: none;
    margin: 1rem;
    cursor: pointer;
  }
  .mark {
    font-size: 1rem;
    line-height: 16px;
  }
  .num {
    line-height: 70px;
    text-align: center;
  }
}
</style>
