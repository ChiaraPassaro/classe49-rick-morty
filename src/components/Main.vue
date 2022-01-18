/* eslint-disable max-len */
/* eslint-disable max-len */
<template>
  <main>
    <div
      class="container"
    >
      <div class="row">
        <div class="col-12">
          <Search
            @doSearch="searchCharacters($event)"
          />
        </div>
      </div>
      <div
        v-if="characters"
        class="row cards"
      >
        <CardNew
          v-for="(card, index) in filteredCharacters"
          :key="index+card.id"
          :image="card.image"
          :image-alt="card.name"
          :heading2="card.name"
          :heading3="card.origin.name"
          :heading4="card.species"
          :class="getClass()"
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
        <!-- <i class="fa-solid fa-circle-notch fa-spin" /> -->
        <font-awesome-icon
          icon="circle-notch"
          spin
        />
      </div>
    </div>
  </main>
</template>

<script>
// https://www.npmjs.com/package/@fortawesome/vue-fontawesome
// importiamo le svg e il componente vue fontawesome
import { library } from '@fortawesome/fontawesome-svg-core';
import { faCircleNotch } from '@fortawesome/free-solid-svg-icons'; // icona da usare icona in camelCase
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';

import axios from 'axios';
import CardNew from './CardNew.vue';
import Search from './Search.vue';

library.add(faCircleNotch);

export default {
  name: 'Main',
  components: {
    CardNew,
    Search,
    FontAwesomeIcon, // inseriamo qui il componente
  },
  data() {
    return {
      textSearch: '',
      characters: null,
      cardsDeck: null,
      queryApiDeck: 'http://deckofcardsapi.com/api/deck/new/draw/?count=4',
      queryApi: 'https://rickandmortyapi.com/api/',
    };
  },
  computed: {
    filteredCharacters() {
      if (this.textSearch === '') {
        return this.characters;
      }

      // eslint-disable-next-line max-len
      return this.characters.filter((element) => element.name.toLowerCase().includes(this.textSearch.toLowerCase()));
    },
  },
  created() {
    console.log('created');
  },
  mounted() {
    console.log('mounted');
    setTimeout(() => {
      this.getCharacters();
    }, 10000);
    this.getCards();
  },
  methods: {
    getCharacters() {
      axios.get(`${this.queryApi}character/`)
        .then((result) => {
          this.characters = result.data.results;
          this.filteredCharacters = result.data.results;
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
    searchCharacters(text) {
      console.log(text);
      this.textSearch = text;
    },
    getClass() {
      console.log('getClass');
      return 'new-class';
    },
  },
};
</script>

<style lang="scss">
 @import '@fortawesome/fontawesome-free';
 .fa-circle-notch {
   font-size: 4em;
 }
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
