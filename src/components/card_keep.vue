<template>
  <div>カード所持数：{{ myCards.length }}</div>
</template>
<script>
export default {
  name: 'my-card',
  data() {
    return {
      
    }
  },
  props: ["myCards"],
  computed() {
    
  }
}
</script>
