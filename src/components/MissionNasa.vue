<script>
export default {
 
  data() {
    return {
      nasaData: null,
      nasaTitle: null,
      nasaExplanation:null,
      nasaDate:null,
      width: 300,
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
    >What happend today? <v-icon icon="mdi-plus"></v-icon
  ></v-btn>
 
  <div v-if="nasaData">

    <h1 class="elements_h">{{ nasaTitle }}</h1>
    <h2 class="elements_h">{{nasaDate}}</h2>
    <h3 class="elements_h"> {{nasaExplanation}}</h3>
    
      <v-img
        class="bg-white"
        width="250"
        :aspect-ratio="1"
        :src="nasaData.url"
      />

  <div class="d-flex flex-column justify-space-between align-center">
    <v-slider
      v-model="width"
      class="align-self-stretch"
      min="200"
      max="500"
      step="1"
    ></v-slider>

    <v-img
      :aspect-ratio="16/9"
      :width="width"
      :src="nasaData.url"
    ></v-img>
  </div>

    
<h4>{{nasaData.copyright}}</h4>

  </div>
</template>

<style scoped>
img {
  float: left;
  margin-right: -160px;
}
h1{
  padding-top: 25px;
  padding-left: 42%;
}

h2{
 padding-left: 90%;
}

</style>
