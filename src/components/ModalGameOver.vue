<template>
  <transition name="fade">
    <div v-if="gameOver" class="modal-stop-game">
      <div class="modal-stop-game__content">
        <h3 class="modal-stop-game__title">Игра окончена</h3>
        <button @click="StartGame" class="modal-stop-game__button">
          Начать заново
        </button>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "modal-game-over",
  props: {
    gameOver: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    StartGame() {
      this.$emit("start-game");
    },
  },
};
</script>

<style lang="scss">
.modal-stop-game {
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: #00000061;
  backdrop-filter: blur(3px);
  &__content {
    width: 100%;
    max-width: 350px;
    background: #3f3f3f;
    gap: 30px;
    padding: 35px 0px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border-radius: 5px;
    box-shadow: 2px 2px 13px 3px #000;
  }
  &__title {
    color: #fafafa;
    font-size: 23px;
    text-align: center;
  }
  &__button {
    padding: 5px 20px;
    border-radius: 5px;
    background-color: #2ebbb4;
    box-shadow: 4px 4px 10px 0px rgba(0, 0, 0, 0.61);
    font-size: 15px;
    transition: background-color 0.1s ease;
    &:hover {
      background-color: #6fd1cc;
    }
  }
}
</style>
