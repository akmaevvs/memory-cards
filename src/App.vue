<template>
  <div id="app">
    <div class="container">
      <div
        class="container__square"
        v-for="(card, index) in cards"
        :key="index"
        @click="flipCard(index)"
      >
        {{ card.id }}
        {{ index }}
        <img
          class="container__img"
          v-if="openAll || card.open || card.findPair"
          :src="card.imgUrl"
          alt
        />
        <!-- <img class="container__img" v-else :src="cardBack" alt /> -->
      </div>
    </div>
  </div>
</template>

<script>
// import axios from "axios";
import cardBack from "@/assets/card-back2.png";
export default {
  name: "App",
  components: "",
  data() {
    return {
      size: 30,
      cardBack,
      openNow: null,
      openAll: true,
      lockCards: false,
      cards: [
        {
          id: 1,
          imgUrl:
            "https://images.unsplash.com/photo-1641921403073-83551d2dd59d?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDF8YkRvNDhjVWh3bll8fGVufDB8fHx8&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        },
        {
          id: 2,
          imgUrl:
            "https://images.unsplash.com/photo-1641982154657-9e5715d6e217?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDJ8YkRvNDhjVWh3bll8fGVufDB8fHx8&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        },
        {
          id: 3,
          imgUrl:
            "https://images.unsplash.com/photo-1641933150680-42cf911265a7?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDN8YkRvNDhjVWh3bll8fGVufDB8fHx8&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        },
        {
          id: 4,
          imgUrl:
            "https://images.unsplash.com/photo-1641341283592-bd8202706545?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDEwfGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        },
        {
          id: 5,
          imgUrl:
            "https://images.unsplash.com/photo-1641666017842-f94246ef2961?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDExfGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        },
        {
          id: 6,
          imgUrl:
            "https://images.unsplash.com/photo-1641603229645-15c56358b6f9?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDE3fGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        },
        {
          id: 7,
          imgUrl:
            "https://images.unsplash.com/photo-1580687580441-96dbadf8f3c8?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDIzfGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        },
        {
          id: 8,
          imgUrl:
            "https://images.unsplash.com/photo-1526726604676-851e8355bd8d?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDM0fGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        },
        {
          id: 9,
          imgUrl:
            "https://images.unsplash.com/photo-1619378927749-3a632de8c3c9?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDQzfGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        },
        {
          id: 10,
          imgUrl:
            "https://images.unsplash.com/photo-1640730518250-ad5fb98b4d9a?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDQ0fGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        },
        {
          id: 11,
          imgUrl:
            "https://images.unsplash.com/photo-1641146294939-c45661731e36?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDQyfGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        },
        {
          id: 12,
          imgUrl:
            "https://images.unsplash.com/photo-1640547587731-f09714209f6b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDQ2fGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        },
        {
          id: 13,
          imgUrl:
            "https://images.unsplash.com/photo-1640098322989-a8680252fb8c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDQ5fGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        },
        {
          id: 14,
          imgUrl:
            "https://images.unsplash.com/photo-1617105106017-8a99f99e6b14?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDUzfGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        },
        {
          id: 15,
          imgUrl:
            "https://images.unsplash.com/photo-1617136908328-03ea35ec3e3d?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDUyfGJEbzQ4Y1Vod25ZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
          open: false,
          findPair: false
        }
      ]
    };
  },
  async mounted() {
    setTimeout(() => {
      this.openAll = false;
    }, 2500);
    // const unsplashPhotos = await axios
    //   .get(`https://jsonplaceholder.typicode.com/albums/1/photos?_limit=15`)
    //   .then((result) => {
    //     if (result.status == 200) {
    //       return result.data;
    //     }
    //   })
    //   .catch((error) => {
    //     if (error.response) {
    //       console.log("err");
    //       console.log(error.response.status);

    //       if (error.response.status === 404) {
    //         console.log(`cannot be found.`);
    //       }
    //     }
    //   });
    //   this.cards.map((el, index) => {
    //     el.img = unsplashPhotos[index]
    //     console.log(index);
    //   })
    //   // this.cards.forEach((element, index) => {
    //     // this.cards[index].img = unsplashPhotos[index]
    //   // });
    // // this.cards.forEach(element => {
    // //   element.img
    // // });

    // console.log(unsplashPhotos);
    console.log(this.cards);
    // console.log(this.cards.concat(this.cards).sort(() => Math.round(Math.random() * 100) - 50));
    for (let index = 0; index < 15; index++) {
      const copyCard = JSON.parse(JSON.stringify(this.cards[index]));
      this.cards.push(copyCard);
    }
    this.cards = this.cards.sort(() => Math.round(Math.random() * 100) - 50);
    console.log(this.cards);
  },
  methods: {
    flipCard(index) {
      if (this.lockCards) {
        return
      }
      console.log(index);
      this.cards[index].open = !this.cards[index].open;

      if (!this.openNow) {
        this.openNow = index;
      } else {
        if (this.cards[this.openNow].id === this.cards[index].id) {
          this.cards[this.openNow].findPair = true;
          this.cards[index].findPair = true;
          this.openNow = null;
        } else {
          this.lockCards = true
          setTimeout(() => {
            this.cards[this.openNow].open = !this.cards[this.openNow].open;
            this.cards[index].open = !this.cards[index].open;
            this.openNow = null;
            this.lockCards = false

          }, 1500);
        }
      }
    }
  }
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

#app {
  background-color: #fafafa;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  overflow: hidden;
  margin: 0;
}

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
    transition: transform 0.2s ease-in;
    color: #fff;
    text-shadow: 1px 2px 2px #000;
    border-radius: 6px;
    // overflow: hidden;
    box-shadow: 1px 1px 2px 2px #000;
    &:hover {
      transform: scale(1.05);
    }
  }
  &__img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}
</style>
