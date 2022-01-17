<template>
  <main>
    <div class="container">
      <div class="row">
        <div class="col-12">
          <div class="search">
            Segnaposto
          </div>
        </div>
      </div>
      <div
        v-if="characters"
        class="row cards"
      >
        <CardNew
          v-for="(card, index) in characters"
          :key="index+card.id"
          :image="card.image"
          :image-alt="card.name"
          :heading2="card.name"
          :heading3="card.origin.name"
          :heading4="card.species"
        />
      </div>
      <!-- <div
          v-for="(card, index) in cards"
          :key="index + card.id"
          class="col-3 p-3 border-0 card"
        >
          <img
            class="rounded-circle shadow mb-3"
            :src="card.image"
            :alt="card.name"
          >
          <h2>
            {{ card.name }}
          </h2>
          <h3 class="fs-6 fw-normal divider-top">
            {{ card.origin.name }}
          </h3>
          <h4 class="fs-5">
            {{ card.species }}
          </h4>
        </div> -->
      <!-- <div class="col-3 card p-3">
          <img
            class="rounded-circle shadow mb-3"
            src="https://rickandmortyapi.com/api/character/avatar/1.jpeg"
            alt="Rick Sanchez"
          >
          <h2>
            Rick Sanchez
          </h2>
          <h3 class="fs-6 fw-normal divider-top">
            Earth (C-137)
          </h3>
          <h4 class="fs-5">
            Human
          </h4>
        </div> -->
      <div v-else>
        <h1>Loading</h1>
      </div>

      <hr>

      <div
        v-if="cardsDeck"
        class="row cards"
      >
        <CardNew
          v-for="(card, index) in cardsDeck"
          :key="index+card.code"
          :image="card.image"
          :image-alt="card.value"
          :heading2="card.value"
          :heading3="card.suit"
          :heading4="card.code"
        />
      </div>
      <div v-else>
        <h1>Loading</h1>
      </div>
    </div>
  </main>
</template>

<script>
import axios from 'axios';
import CardNew from './CardNew.vue';

// result {
//     "info": {
//     },
//     "results": [
//         {
//             "id": 1,
//             "name": "Rick Sanchez",
//             "status": "Alive",
//             "species": "Human",
//             "type": "",
//             "gender": "Male",
//             "origin": {
//                 "name": "Earth (C-137)",
//                 "url": "https://rickandmortyapi.com/api/location/1"
//             },
//             "location": {
//                 "name": "Citadel of Ricks",
//                 "url": "https://rickandmortyapi.com/api/location/3"
//             },
//             "image": "https://rickandmortyapi.com/api/character/avatar/1.jpeg",
//             "episode": [
//             ],
//             "url": "https://rickandmortyapi.com/api/character/1",
//             "created": "2017-11-04T18:48:46.250Z"
//         },

export default {
  name: 'Main',
  components: {
    CardNew,
  },
  data() {
    return {
      characters: null,
      cardsDeck: null,
      queryApiDeck: 'http://deckofcardsapi.com/api/deck/new/draw/?count=4',
      queryApi: 'https://rickandmortyapi.com/api/',
    };
  },
  created() {
    console.log('created');
  },
  mounted() {
    console.log('mounted');
    // simuliamo una chiamata con ritardo
    // setTimeout(() => {
    //   axios.get('https://rickandmortyapi.com/api/character/')
    //     .then((result) => {
    //       console.log(result.data.results);
    //       this.cards = result.data.results;
    //     })
    //     .catch((error) => {
    //       console.log(error);
    //     });
    // }, 1000);
    this.getCharacters();
    this.getCards();
  },
  methods: {
    getCharacters() {
      axios.get(`${this.queryApi}character/`)
        .then((result) => {
        // console.log();
        // const { results } = result.data;
        // const data = results.map((element) => {
        //   const {
        //     name, image, origin, species,
        //   } = element;
        //   return {
        //     name, image, origin, species,
        //   };
        // });

          // console.log(data);

          this.characters = result.data.results;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getCards() {
      axios.get(this.queryApiDeck)
        .then((result) => {
          console.log(result.data.cards);
          this.cardsDeck = result.data.cards;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style lang="scss">
  .card {
    .divider-top::before {
      content: '';
      position: relative;
      left: 50%;
      transform: translateX(-50%);
      display: block;
      width: 50%;
      height: 2px;
      margin-bottom: 1em;
      background-color: black;
    }
  }
</style>
