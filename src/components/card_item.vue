<template>
  <div id="">
    <div :class="{ 'card-items-front': card.isFront, 'card-items-reverse': !card.isFront}">
      <span class="card-item-number" v-if="card.isFront">{{card.mark}}{{card.number}}</span>
    </div>
  </div>
</template>

<script>

export default {
  name: 'card-item',
  props: ["card"],
  data() {
    return {
      cardStatus: false,
    }
  },

}
</script>

<style scoped>
.card-item-number {
    position: absolute;
    top: 50%;
    right: 28%;
    transform: translateY(-50%);
    font-size: 18px;
}
.card-items-reverse {
  display: block;
}
.card-items-reverse:before {
  font-family: "Font Awesome 5 Free";
  content: "\f6be";
  font-size: 26px;
  font-weight: bold;
  position: absolute;
  top: 50%;
  right: 29%;
  transform: translateY(-50%);
}
.card-items-front {
  display: block;
}
.card-items-front:before {
  position: absolute;
  top: 41%;
  right: 46%;
  background-color: aliceblue;
}
</style>