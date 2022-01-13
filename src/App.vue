<template>
  <div id="app">
    <div class="container">
      <div
        class="container__square"
        v-for="(card, index) in cards"
        :key="index"
      >
        {{ card.id }}
        <img width="10" height="10" :src="card.img.url" alt="">
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  components: {},
  data() {
    return {
      size: 30,
      cards: [
        {
          id: 1,
          img: {},
        },
        {
          id: 2,
          img: {},
        },
        {
          id: 3,
          img: {},
        },
        {
          id: 4,
          img: {},
        },
        {
          id: 5,
          img: {},
        },
        {
          id: 6,
          img: {},
        },
        {
          id: 7,
          img: {},
        },
        {
          id: 8,
          img: {},
        },
        {
          id: 9,
          img: {},
        },
        {
          id: 10,
          img: {},
        },
        {
          id: 11,
          img: {},
        },
        {
          id: 12,
          img: {},
        },
        {
          id: 13,
          img: {},
        },
        {
          id: 14,
          img: {},
        },
        {
          id: 15,
          img: {},
        },
      ],
    };
  },
  async mounted() {
    const unsplashPhotos = await axios
      .get(`https://jsonplaceholder.typicode.com/albums/1/photos?_limit=15`)
      .then((result) => {
        if (result.status == 200) {
          return result.data;
        }
      })
      .catch((error) => {
        if (error.response) {
          console.log("err");
          console.log(error.response.status);

          if (error.response.status === 404) {
            console.log(`cannot be found.`);
          }
        }
      });
      this.cards.map((el, index) => {
        el.img = unsplashPhotos[index]
        console.log(index);
      })
      // this.cards.forEach((element, index) => {
        // this.cards[index].img = unsplashPhotos[index]
      // });
    // this.cards.forEach(element => {
    //   element.img
    // });

    console.log(unsplashPhotos);
    console.log(this.cards);
    // console.log(this.cards.concat(this.cards).sort(() => Math.round(Math.random() * 100) - 50));
    this.cards = this.cards
      .concat(this.cards)
      .sort(() => Math.round(Math.random() * 100) - 50);
  },
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
    width: 90px;
    height: 90px;
    background: #1d1d1d;
    cursor: pointer;
    transition: transform 0.2s ease-in;
    color: #fff;
    &:hover {
      transform: scale(1.05);
    }
  }
}
</style>
