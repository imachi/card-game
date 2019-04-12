<template>
  <div id="app" :class="{isLock: locking}">
    <div class="card-area" v-for="(cardLines, index) in shuffledCards" :key="index">
      <template v-for="(card, index) in cardLines">
        <div class="card-item" @click="onClickCard(card)" :class="{ 'is-display-hidden': !card.existence }" :key="index">
          <CardItems :card="card"></CardItems>
        </div>
      </template>
    </div>
    <div class="my-card">
      <CardKeep :myCards="myCards"></CardKeep>
    </div>
  </div>
</template>


<script>
import CardItems from './components/card_item';
import CardKeep from './components/card_keep';

const shuffle = ([...arr]) => {
    let m = arr.length;
    while (m) {
      const i = Math.floor(Math.random() * m--);
      [arr[m], arr[i]] = [arr[i], arr[m]];
    }
    return arr;
  };

function sleep(time) {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve();
    }, time);
  });
}

export default {
  name: 'app',
  data() {
    return {
      cards: [
        [{mark: "♡", number: 1, isFront: false, existence: true}, {mark: "♡", number: 2, isFront: false, existence: true}, {mark: "♡", number: 3, isFront: false, existence: true}, {mark: "♡", number: 4, isFront: false, existence: true}, {mark: "♡", number: 5, isFront: false, existence: true}, {mark: "♡", number: 6, isFront: false, existence: true}, {mark: "♡", number: 7, isFront: false, existence: true}, {mark: "♡", number: 8, isFront: false, existence: true}, {mark: "♡", number: 9, isFront: false, existence: true}, {mark: "♡", number: 10, isFront: false, existence: true}, {mark: "♡", number: 11, isFront: false, existence: true}, {mark: "♡", number: 12, isFront: false, existence: true}, {mark: "♡", number: 13, isFront: false, existence: true}],
        [{mark: "♢", number: 1, isFront: false, existence: true}, {mark: "♢", number: 2, isFront: false, existence: true}, {mark: "♢", number: 3, isFront: false, existence: true}, {mark: "♢", number: 4, isFront: false, existence: true}, {mark: "♢", number: 5, isFront: false, existence: true}, {mark: "♢", number: 6, isFront: false, existence: true}, {mark: "♢", number: 7, isFront: false, existence: true}, {mark: "♢", number: 8, isFront: false, existence: true}, {mark: "♢", number: 9, isFront: false, existence: true}, {mark: "♢", number: 10, isFront: false, existence: true}, {mark: "♢", number: 11, isFront: false, existence: true}, {mark: "♢", number: 12, isFront: false, existence: true}, {mark: "♢", number: 13, isFront: false, existence: true}],
        [{mark: "♠︎", number: 1, isFront: false, existence: true}, {mark: "♠︎", number: 2, isFront: false, existence: true}, {mark: "♠︎", number: 3, isFront: false, existence: true}, {mark: "♠︎", number: 4, isFront: false, existence: true}, {mark: "♠︎", number: 5, isFront: false, existence: true}, {mark: "♠︎", number: 6, isFront: false, existence: true}, {mark: "♠︎", number: 7, isFront: false, existence: true}, {mark: "♠︎", number: 8, isFront: false, existence: true}, {mark: "♠︎", number: 9, isFront: false, existence: true}, {mark: "♠︎", number: 10, isFront: false, existence: true}, {mark: "♠︎", number: 11, isFront: false, existence: true}, {mark: "♠︎", number: 12, isFront: false, existence: true}, {mark: "♠︎", number: 13, isFront: false, existence: true}],
        [{mark: "♧", number: 1, isFront: false, existence: true}, {mark: "♧", number: 2, isFront: false, existence: true}, {mark: "♧", number: 3, isFront: false, existence: true}, {mark: "♧", number: 4, isFront: false, existence: true}, {mark: "♧", number: 5, isFront: false, existence: true}, {mark: "♧", number: 6, isFront: false, existence: true}, {mark: "♧", number: 7, isFront: false, existence: true}, {mark: "♧", number: 8, isFront: false, existence: true}, {mark: "♧", number: 9, isFront: false, existence: true}, {mark: "♧", number: 10, isFront: false, existence: true}, {mark: "♧", number: 11, isFront: false, existence: true}, {mark: "♧", number: 12, isFront: false, existence: true}, {mark: "♧", number: 13, isFront: false, existence: true}]
      ],
      shuffledCards: [],
      selectedCards: [],
      myCards: [],
      locking: false
    }
  },

  components: {
    CardItems,
    CardKeep,
  },

  created() {
    const shuffledCards = shuffle(this.cards.flat());
    this.shuffledCards[0] = [...shuffledCards].splice(0, 13); 
    this.shuffledCards[1] = [...shuffledCards].splice(13, 13); 
    this.shuffledCards[2] = [...shuffledCards].splice(26, 13); 
    this.shuffledCards[3] = [...shuffledCards].splice(39, 13); 
  }, 
  methods: {
    async onClickCard(card) {
      card.isFront = !card.isFront;
      this.selectedCards.push(card);

      if (this.selectedCards.length === 2) { // TODO カードの数字を比較
        this.locking = true;
        const firstCard = this.selectedCards[0];
        const secondCard = this.selectedCards[1];
        
        if (firstCard.number === secondCard.number) {
          await sleep(2000);
          firstCard.existence = false;
          secondCard.existence = false;
          this.myCards.push(firstCard, secondCard);
          this.selectedCards = [];
        } else {
          await sleep(2000);
          firstCard.isFront = false;
          secondCard.isFront = false;
          this.selectedCards = [];
        }
        this.locking = false;
      }
    },
  },
}
</script>

<style scoped>
.card-area {
  display: flex;
}
.card-item {
  width: 59px;
  height: 86px;
  border: solid 1px black;
  border-radius: 5px;
  position: relative;
  margin: 10px;
  background-color: #fff;
}
.is-display-hidden {
  visibility: hidden;
}
.isLock {
  pointer-events: none;
}
</style>
