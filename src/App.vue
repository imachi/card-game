<template>
  <div id="app">
    <div class="card-area" v-for="(cardLines, index) in cards" :key="index">
      <template v-for="(card, index) in cardLines">
        <div class="card-item" @click="onClickCard(card)" :class="{ 'is-display-hidden': !card.existence }" :key="index">
          <CardItems :card="card"></CardItems>
        </div>
      </template>
      </div>
    <CardKeep></CardKeep>
  </div>
</template>


<script>
import CardItems from './components/card_item';
import CardKeep from './components/card_keep';

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
      selectedCards: [],
    }
  },
  created() {
    let array;
    for(var item = 0; this.cards.length > item; item++) {
      array = this.cards[item];

      for(var l = array.lengtn -1; l > 0; l--) {
        const m = Math.floor(Math.random() * (i +1));
        [array[m], array[l]] = [array[l], array[m]]
        return array;
      }
      console.log(array);
    }
    
    const cardRow = [this.cards[0][0], this.cards[1][0], this.cards[2][0], this.cards[3][0]];
    // TODO newAryをシャッフル
    this.cards[0, 0] = cardRow[0, 0];
    this.cards[1, 0] = cardRow[1, 0];
    this.cards[2, 0] = cardRow[2, 0];
    this.cards[3, 0] = cardRow[3, 0];
  },
  components: {
    CardItems,
  },
  methods: {
    async onClickCard(card) {
      card.isFront = !card.isFront;
      this.selectedCards.push(card);

      if (this.selectedCards.length === 2) { // TODO カードの数字を比較
        const firstCard = this.selectedCards[0];
        const secondCard = this.selectedCards[1];
        
        if (firstCard.number === secondCard.number) {
          await sleep(1000);
          firstCard.existence = false;
          secondCard.existence = false;
          this.selectedCards = [];
        } else {
          await sleep(1000);
          firstCard.isFront = false;
          secondCard.isFront = false;
          this.selectedCards = [];
        }
      }
    },
  },
  mounted: {

  }
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
</style>
