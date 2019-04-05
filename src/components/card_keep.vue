<template>
  <div>{{ myCard.length }}</div>
</template>
<script>
export default {
  data() {
    return {
      myCard: [],
    }
  },
  props: ["myCard"],
  computed() {
    
  }
}
</script>
