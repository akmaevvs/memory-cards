<template>
  <div id="app">
    <container-cards
      :gameCards="gameCards"
      :openAll="openAll"
      @flip-card="flipCard"
    />
    <modal-game-over :gameOver="gameOver" @start-game="StartGame" />
  </div>
</template>

<script>
import ContainerCards from "@/components/ContainerCards.vue";
import ModalGameOver from "@/components/ModalGameOver.vue";

export default {
  components: { ContainerCards, ModalGameOver },
  name: "App",
  data() {
    return {
      openNow: null,
      openAll: true,
      lockCards: false,
      countOpen: 0,
      gameOver: false,
      cards: [
        {
          id: 1,
          imgUrl:
            "https://images.unsplash.com/photo-1641921403073-83551d2dd59d?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDF8YkRvNDhjVWh3bll8fGVufDB8fHx8&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
        {
          id: 2,
          imgUrl:
            "https://images.unsplash.com/photo-1641982154657-9e5715d6e217?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDJ8YkRvNDhjVWh3bll8fGVufDB8fHx8&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
        {
          id: 3,
          imgUrl:
            "https://images.unsplash.com/photo-1641933150680-42cf911265a7?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDN8YkRvNDhjVWh3bll8fGVufDB8fHx8&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
        {
          id: 4,
          imgUrl:
            "https://images.unsplash.com/photo-1641341283592-bd8202706545?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDEwfGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
        {
          id: 5,
          imgUrl:
            "https://images.unsplash.com/photo-1641666017842-f94246ef2961?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDExfGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
        {
          id: 6,
          imgUrl:
            "https://images.unsplash.com/photo-1641603229645-15c56358b6f9?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDE3fGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
        {
          id: 7,
          imgUrl:
            "https://images.unsplash.com/photo-1580687580441-96dbadf8f3c8?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDIzfGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
        {
          id: 8,
          imgUrl:
            "https://images.unsplash.com/photo-1526726604676-851e8355bd8d?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDM0fGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
        {
          id: 9,
          imgUrl:
            "https://images.unsplash.com/photo-1619378927749-3a632de8c3c9?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDQzfGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
        {
          id: 10,
          imgUrl:
            "https://images.unsplash.com/photo-1640730518250-ad5fb98b4d9a?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDQ0fGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
        {
          id: 11,
          imgUrl:
            "https://images.unsplash.com/photo-1641146294939-c45661731e36?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDQyfGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
        {
          id: 12,
          imgUrl:
            "https://images.unsplash.com/photo-1640547587731-f09714209f6b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDQ2fGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
        {
          id: 13,
          imgUrl:
            "https://images.unsplash.com/photo-1640098322989-a8680252fb8c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDQ5fGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
        {
          id: 14,
          imgUrl:
            "https://images.unsplash.com/photo-1617105106017-8a99f99e6b14?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDUzfGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
        {
          id: 15,
          imgUrl:
            "https://images.unsplash.com/photo-1617136908328-03ea35ec3e3d?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDUyfGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false,
        },
      ],
      gameCards: [],
    };
  },
  watch: {
    countOpen: function (val) {
      if (val == 15) {
        this.gameOver = true;
      }
    },
  },
  async mounted() {
    this.StartGame();
  },
  methods: {
    StartGame() {
      this.gameOver = false;
      this.countOpen = 0;
      this.lockCards = true;
      this.openAll = true;
      
      this.gameCards = this.cards.map((a) => {
        return { ...a };
      });
      for (let index = 0; index < 15; index++) {
        const copyCard = JSON.parse(JSON.stringify(this.gameCards[index]));
        this.gameCards.push(copyCard);
      }
      this.gameCards = this.gameCards.sort(
        () => Math.round(Math.random() * 100) - 50
      );

      setTimeout(() => {
        this.lockCards = false;
        this.openAll = false;
      }, 2500);
    },
    flipCard(index) {
      if (this.lockCards) {
        return;
      }
      this.gameCards[index].open = !this.gameCards[index].open;
      if (this.openNow == null) {
        this.openNow = index;
      } else {
        this.matchCards(this.openNow, index);
      }
    },
    matchCards(openNow, index) {
      if (
        this.gameCards[openNow].id === this.gameCards[index].id &&
        index !== openNow
      ) {
        this.gameCards[openNow].findPair = true;
        this.gameCards[index].findPair = true;
        this.openNow = null;
        this.countOpen++;
      } else {
        this.lockCards = true;
        setTimeout(() => {
          this.gameCards[openNow].open = !this.gameCards[openNow].open;
          this.gameCards[index].open = !this.gameCards[index].open;
          this.openNow = null;
          this.lockCards = false;
        }, 1500);
      }
    },
  },
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

button {
  border: 0;
  outline: none;
  white-space: nowrap;
  cursor: pointer;
}
.fade-enter-active {
  transition-property: opacity;
  transition-duration: 0.2s;
  transition-delay: 0.2s;
}
.fade-leave-active {
  transition-property: opacity;
  transition-duration: 0.2s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
#app {
  background-color: #111;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  overflow: hidden;
  margin: 0;
}
.flip {
  transition: transform 0.3s ease-in;
  transform: rotateY(180deg);
}
</style>
