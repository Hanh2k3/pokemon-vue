<template>
  <div
    class="card"
    :class="{ enable: isEnabled }"
    @click="onToggleFlipCard()"
    :style="{
      height: `${(920 - 16 * 4) / Math.sqrt(cardContext.length) - 16}px`,
      width: `${
        (((920 - 16 * 4) / Math.sqrt(cardContext.length) - 16) * 3) / 4
      }px`,
    }"
  >
    <div class="card__inner" :class="{ is__flip: isFlipped }">
      <div class="card__face card__face--front">
        <div
          class="card__content"
          :style="{
            backgroundSize: `${
              (((920 - 16 * 4) / Math.sqrt(cardContext.length) - 16) * 1) / 3
            }px ${
              (((920 - 16 * 4) / Math.sqrt(cardContext.length) - 16) * 1) / 4
            }px`,
          }"
        ></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('@/assets/images/' +
              backImageUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isFlipped: false,
      isEnabled: false,
    };
  },
  props: {
    card: {
      type: [Array, String, Number, Boolean, Object],
      required: true,
    },
    backImageUrl: {
      type: String,
      required: true,
    },
    cardContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  methods: {
    onToggleFlipCard() {
      if (this.isEnabled) return false;
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) {
        this.$emit("onFlip", this.card);
      }
    },
    onFlipBackCard() {
      this.isFlipped = false;
    },
    onEnabled() {
      this.isEnabled = true;
    },
  },
};
</script>

<style lang="css" scoped>
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
}
.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}

.card.enable .card__inner {
  cursor: default;
}
.card__inner.is__flip {
  transform: rotateY(-180deg);
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0px 3px 10px 3px rgba(0, 0, 0, 0.2);
}
.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
.card__face--back .card__content {
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center center;
  width: 100%;
  height: 100%;
}
.card__face--front .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center;
  height: 100%;
  width: 100%;
}
</style>
