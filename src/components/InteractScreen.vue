<template>
  <div class="screen">
    <div
      class="screen_inner"
      :style="{
        width: `${
          ((((920 - 16 * 4) / Math.sqrt(cardsContext.length) + 16) * 3) / 4) *
          Math.sqrt(cardsContext.length)
        }px`,
      }"
    >
      <card-flip
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :backImageUrl="`${card}.png`"
        :card="{ index, value: card }"
        :cardContext="cardsContext"
        @onFlip="checkRule($event)"
      />
    </div>
  </div>
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
  data() {
    return {
      rules: [],
      numberCardFlipped: 0,
    };
  },
  methods: {
    getCard(index) {
      return `card-${index}`;
    },
    checkRule(card) {
      if (this.rules.length === 2) return false;
      // when not full
      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        // make card not toggle
        this.$refs[`card-${this.rules[0].index}`][0].onEnabled();
        this.$refs[`card-${this.rules[1].index}`][0].onEnabled();
        // reset rule
        this.rules = [];
        //check when success game
        this.numberCardFlipped += 2;
        console.log(this.numberCardFlipped);
        if (this.numberCardFlipped === this.cardsContext.length) {
          this.$emit("onEnd");
        }
      } else {
        if (
          this.rules.length === 2 &&
          this.rules[0].value !== this.rules[1].value
        ) {
          setTimeout(() => {
            // close two card
            this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
            this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
            // reset rules
            this.rules = [];
          }, 800);
        } else return false;
      }
    },
  },
};
</script>

<style lang="css" scoped>
.screen {
  width: 100%;
  height: 100vh;
  background-color: var(--dark);
  position: absolute;
  top: 0;
  right: 0;
  margin: 0;
}
.screen_inner {
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
