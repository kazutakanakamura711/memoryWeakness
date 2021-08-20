<template>
<div class="main">
  <Cards
    :cardsArr="cardsArr"
    @open="open"
  />
  <div v-show="displayMessage.endFlag">
    <DisplayMessage
    class="message"
    :message="displayMessage.message"
  />
  </div>
  <div class="bottom">
    <StartBtn
      @countStart="countStart"
      :showStartBtn="showStartBtn"
      class="startBtn"
    />
  </div>
  <Time
    :name="name"
  />
  <Record
    :time="time.start"
    class="record"
  />
  <ReloadBtn
    :endFlag="displayMessage.endFlag"
    :nameReload="nameReload"
    @reload="reload"
  />
  <Title
    :title="title"
    class="title"
  />
</div>
</template>

<script>
export default {
  data() {
    return {
      cardsNumSpade: [],
      cardsNumHeart: [],
      cardsNumClub: [],
      cardsNumDia: [],
      cardsArr: [],
      openCards: {
        right: true,
        count: 0,
        cards: [],
      },
      time: {
        countFlg: false,
        start: 0,
        clearId: '',
      },
      delCardsArr: [],
      showStartBtn: true,
      displayMessage: {
        message: 'COMPLETE!!',
        endFlag: false,
      },
      title: 'MemoryWeakness',
      name: 'TIME',
      nameReload: 'RELOAD',
    };
  },
  methods: {
    makeCardsArr(id,n) {
      this.cardsNumSpade.push({ id: id, mark: '♠', num: n, isBlack: false, isRed: false, isOpen: false, isDisabled: true, isDel: false,});
      this.cardsNumHeart.push({ id: id*2, mark: '♥', num: n, isBlack: false, isRed: false, isOpen: false, isDisabled: true, isDel: false,});
      this.cardsNumClub.push({ id: id*3, mark: '♣', num: n, isBlack: false, isRed: false, isOpen: false, isDisabled: true, isDel: false,});
      this.cardsNumDia.push({ id: id*4, mark: '♦', num: n, isBlack: false, isRed: false, isOpen: false, isDisabled: true, isDel: false,});
    },
    shuffle(array) {
      for (var i = array.length - 1; 0 < i; i--) {
        // 0〜(i+1)の範囲で値を取得
        var r = Math.floor(Math.random() * (i + 1));

        // 要素の並び替えを実行
        var tmp = array[i];
        array[i] = array[r];
        array[r] = tmp;
      }
      return array;
    },
    countStart() {
      if (this.time.countFlg) {
        return
      }
      this.time.countFlg = true
      for (let i = 0; i < this.cardsArr.length; i++) {
        this.cardsArr[i]['isDisabled'] = false
      }
      this.showStartBtn = false
      var t = 0
      this.time.clearId = setInterval(() => {
        t++
        this.time.start = `${(t/10).toFixed(1)}sec`
      },100)
    },
    open(index) {
      if (this.cardsArr[index]['isDisabled']) {
        return
      }
      if(!this.openCards.right) {
        return
      }
      if (this.openCards.count == 0 || 1) {
        this.openCards.count++
        this.cardsArr[index]['isOpen'] = true
        this.openSE()
        if (this.cardsArr[index]['mark'] == '♦') {
          this.cardsArr[index]['isRed'] = true
        }
        if (this.cardsArr[index]['mark'] == '♥') {
          this.cardsArr[index]['isRed'] = true
        }
        this.openCards.cards.push(this.cardsArr[index])
        this.cardsArr[index]['isDisabled'] = true
      }
      if (this.openCards.count == 2) {
        this.openCards.count = 0
        this.openCards.right = false
        if (this.openCards.cards[0]['num'] == this.openCards.cards[1]['num']) {
          setTimeout(() => {
            this.openCards.cards[0]['isDel'] = true
            this.openCards.cards[1]['isDel'] = true
            this.okSE()
            this.delCardsArr.push(this.openCards[0])
            this.delCardsArr.push(this.openCards[1])
            this.endCheck()
          },500)
        }
        setTimeout(() => {
          this.openCards.cards[0]['isDisabled'] = false
          this.openCards.cards[0]['isOpen'] = false
          this.openCards.cards[0]['isBlack'] = false
          this.openCards.cards[0]['isRed'] = false
          this.openCards.cards[1]['isDisabled'] = false
          this.openCards.cards[1]['isOpen'] = false
          this.openCards.cards[1]['isBlack'] = false
          this.openCards.cards[1]['isRed'] = false
          this.openCards.cards.length = 0
          this.openCards.right = true
        },600)
      }
    },
    endCheck() {
      if (this.delCardsArr.length == this.cardsArr.length) {
        clearInterval(this.time.clearId)
        this.displayMessage.endFlag = true
        this.cardEndSE()
      }
    },
    reload() {
      location.reload()
    },
    okSE() {
      const okSE = new Audio()
      okSE.preload = "auto"
      okSE.src = "music/okSE.mp3"
      okSE.load()
      okSE.volume = 0.1
      okSE.play()
    },
    openSE() {
      const openSE = new Audio()
      openSE.preload = "auto"
      openSE.src = "music/cardOpenSE.mp3"
      openSE.load()
      openSE.volume = 0.1
      openSE.play()
    },
    cardEndSE() {
      const endSE = new Audio()
      endSE.preload = "auto"
      endSE.src = "music/cardEndSE.mp3"
      endSE.load()
      endSE.volume = 0.1
      endSE.play()
    }
  },
  mounted() {
    for (let i = 1; i <= 13; i++) {
      if (i <= 10) {
        this.makeCardsArr(i,i);
      }
      if (i == 11) {
        this.makeCardsArr(i,"J");
      }
      if (i == 12) {
        this.makeCardsArr(i,"Q");
      }
      if (i == 13) {
        this.makeCardsArr(i,"K");
      }
    }
    this.cardsArr = this.cardsNumSpade.concat(
      this.cardsNumHeart,
      this.cardsNumClub,
      this.cardsNumDia
    )
    this.shuffle(this.cardsArr)
  },
};
</script>

<style scoped>

  .main {
    background: black;
    position: relative;
  }
  .bottom {
    display: flex;
  }
  .record {
    margin: 0 auto;
  }
  .startBtn {
    position: absolute;
    top: 20%;
    left: 11.8em;
  }
  .message {
    position: absolute;
    top: 20%;
    left: 9.1em;
  }
  .title {
    font-size: 0.9em;
  }
  

  @media screen and (min-width: 400px) {
    .startBtn {
      position: absolute;
      top: 20%;
      left: 13.4em;
    }
    .message {
      position: absolute;
      top: 20%;
      left: 10.93em;
    }
  }
  @media screen and (min-width: 481px) {
    .startBtn {
      position: absolute;
      top: 20%;
      left: 32.5em;
    }
    .message {
      position: absolute;
      top: 20%;
      left: 26.5em;
    }
  }
  @media screen and (min-width: 750px) {
    .startBtn {
      position: absolute;
      top: 20%;
      left: 15.2em;
    }
    .message {
      position: absolute;
      top: 20%;
      left: 9.2em;
    }
  }
  @media screen and (min-width: 1000px) {
    .startBtn {
      position: absolute;
      top: 20%;
      left: 22.6em;
    }
    .message {
      position: absolute;
      top: 20%;
      left: 16.8em;
    }
  }
  @media screen and (min-width: 1300px) {
    .startBtn {
      position: absolute;
      top: 20%;
      left: 32.5em;
    }
    .message {
      position: absolute;
      top: 20%;
      left: 26.45em;
    }
  }
  @media screen and (min-width: 1400px) {
    .startBtn {
      position: absolute;
      top: 20%;
      left: 34.6em;
    }
    .message {
      position: absolute;
      top: 20%;
      left: 28.55em;
    }
  }

</style>
