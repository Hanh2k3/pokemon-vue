<template>
  <h1>this is interact ....</h1>
  <card-flip
    v-for="(card, index) in cardsContext"
    :key="index"
    :backImageUrl="`${card}.png`"
  />
</template>

<script>
import CardFlip from "./CardFlip.vue";
export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CardFlip,
  },
};
</script>
