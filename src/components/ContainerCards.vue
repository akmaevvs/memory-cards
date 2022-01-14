<template>
  <div class="container">
    <div
      class="container__square"
      :class="{ flip: card.open || openAll }"
      v-for="(card, index) in gameCards"
      :key="index"
      @click="flipCard(index)"
      :id="index"
    >
      <transition name="fade">
        <img
          class="container__img"
          v-if="openAll || card.open || card.findPair"
          :src="card.imgUrl"
          alt
        />
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  name: "container-cards",
  props: {
    gameCards: {
      type: Array,
      default: () => [],
    },
    openAll: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    flipCard(index) {
      const curCard = this.gameCards[index]
      if (curCard.open || curCard.flipCard) {
        return
      }
      this.$emit("flip-card", index);
    },
  },
};
</script>

<style lang="scss">
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  max-width: 600px;
  flex-wrap: wrap;
  gap: 10px;

  &__square {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 90px;
    height: 120px;
    background: #1d1d1d;
    cursor: pointer;
    transition-property: transform, box-shadow;
    transition: 0.3s ease-in;
    color: #fff;
    text-shadow: 1px 2px 2px #000000;
    border-radius: 6px;
    overflow: hidden;
    box-shadow: 0px 0px 2px 2px #000000b0;
    background-image: url("~@/assets/card-back.png");
    background-size: 50%;
    background-repeat: no-repeat;
    background-position: center;
    &:hover {
      box-shadow: 0px 0px 2px 2px #2ebbb4;
    }
  }
  &__img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}
</style>
