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
  setTimeout(() => {

  }, time);
}

export default {
  name: 'app',
  data() {
    return {
      cards: [
        [{mark: "♡", number: 3, isFront: false, existence: true}, {mark: "♤", number: 10, isFront: false, existence: true}, {mark: "♧", number: 6, isFront: false, existence: true}],
        [{mark: "♢", number: 5, isFront: false, existence: true}, {mark: "♧", number: 11, isFront: false, existence: true}, {mark: "♡", number: 12, isFront: false, existence: true}],
        [{mark: "♢", number: 1, isFront: false, existence: true}, {mark: "♤", number: 6, isFront: false, existence: true}, {mark: "♡", number: 2, isFront: false, existence: true}]
      ],
      selectedCards: [],
    }
  },
  components: {
    CardItems,
  },
  methods: {
    onClickCard(card) {
      card.isFront = !card.isFront;
      this.selectedCards.push(card);

      if (this.selectedCards.length === 2) { // TODO カードの数字を比較
        
        const firstCard = this.selectedCards[0];
        const secondCard = this.selectedCards[1];
        if (firstCard.number === secondCard.number) { // 一緒だった時
          firstCard.existence = false;
          secondCard.existence = false;
          this.selectedCards = [];
        }else { //外れた時 
          setTimeout(stateChange, 1000);          
          function stateChange() {
            firstCard.isFront = false;
            secondCard.isFront = false;
          }
          this.selectedCards = [];
        }
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
</style>
