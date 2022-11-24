<script>
export default {
  data() {
    return {
      nasaData: null,
      nasaTitle: null,
      nasaExplanation:null,
      nasaDate:null,
    };
  },
  methods: {
    fetchNasa() {
      const Url =
        "https://api.nasa.gov/planetary/apod?api_key=sLV88CdBRYRX7E27aeuop6y8fyY1SXNkDkKzDyvD";
      fetch(Url)
        .then((response) => response.json())
        .then((data) => {
          this.nasaData = data;
          this.nasaTitle = data.title;
          this.nasaExplanation=data.explanation;
          this.nasaDate=data.date;
        });
    },

    // fetchCard(deckId) {
    //   const Url = `https://deckofcardsapi.com/api/deck/${deckId}/draw/?count=1`;
    //   fetch(Url)
    //     .then((response) => response.json())
    //     .then((data) => {
    //       this.cardData = data;
    //       this.deckCardsData = [];
    //     });
    // },
    // fetchAllCards(deckId, remaining) {
    //   const Url = `https://deckofcardsapi.com/api/deck/${deckId}/draw/?count=
    //     ${remaining}`;
    //   fetch(Url)
    //     .then((response) => response.json())
    //     .then((data) => {
    //       this.deckCardsData = data.cards;
    //     });
    // },
  },
};
</script>

<template>
  <v-btn @click="fetchNasa"
    >Get my Deck <v-icon icon="mdi-plus"></v-icon
  ></v-btn>
  {{ $data }}

  <div v-if="nasaData">
    <h1>{{ nasaTitle }}</h1>
    <h2>{{nasaDate}}</h2>
    <h3> {{nasaExplanation}}
    
      <v-img
        class="bg-white"
        width="100"
        :aspect-ratio="1"
        :src="nasaData.url"
      />
    </h3>
<h4>{{nasaData.copyright}}</h4>

  </div>





  <div v-if="deckData">
    <v-btn variant="outlined" @click="fetchCard(deckData.deck_id)"
      >Get my Card<v-icon icon="mdi-atom"></v-icon
    ></v-btn>
    <div v-if="cardData">
      <v-img
        class="bg-white"
        width="100"
        :aspect-ratio="1"
        :src="cardData.cards[0].image"
      />
    </div>
    <v-btn
      variant="tonal"
      @click="fetchAllCards(deckData.deck_id, deckData.remaining)"
    >
      Get all Cards <v-icon icon="mdi-auto-fix"></v-icon>
    </v-btn>
    <v-row v-if="deckCardsData.length > 0">
      <v-col
        v-for="(card, index) in deckCardsData"
        :key="index"
        class="d-flex child-flex"
        cols="2"
      >
        <v-img
          class="bg-grey-lighten-2"
          cover
          :aspect-ratio="0"
          :src="card.image"
        />
      </v-col>
    </v-row>
  </div>
</template>

<style scoped>
img {
  float: left;
  margin-right: -160px;
}
</style>
