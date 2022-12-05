<template>
  <div id="app">
    <HeaderPage @getSearchQuery="getSrcQuery" />
    <MainPage :foundFilm="movieArray" :foundSeries="tvSeriesArray" :sState="searchState" />
  </div>
</template>

<script>
import axios from 'axios';
import HeaderPage from './components/HeaderPage.vue';
import MainPage from './components/MainPage.vue';

export default {
  name: 'App',
  components: {
    HeaderPage,
    MainPage,
  },

  data() {
    return {
      srcQuery: '',
    // Array Risultati
      movieArray: [],
      tvSeriesArray: [],
    // API Info
      apiLink:'https://api.themoviedb.org/3',
      apiKey:'eabc937f0d1a54d3a86607d981258abc',
    // Stato richiesta
      apiLang:'it-IT',
      reqState: 'loading',
    // Stato ricerca
      searchState: 'empty',
    }
  },

  methods: {
    getSrcQuery (query) {
      this.srcQuery = query.toLowerCase().trim();
      this.callApi();
    },

    async callApi() {
      try {
      // Chiamata API
        const responseMovie = await axios.get(this.apiLink + '/search/movie?api_key=' + this.apiKey + '&query=' +this.srcQuery + '&language=' + this.apiLang);
        const responseTvSeries = await axios.get(this.apiLink + '/search/tv?api_key=' + this.apiKey + '&query=' +this.srcQuery + '&language=' + this.apiLang);
      // Array Risultati
        this.movieArray = responseMovie.data.results;
        this.tvSeriesArray = responseTvSeries.data.results;
      // Controllo Array Risultati Film
        if (this.movieArray.length == 0) {
          this.searchState = 'notFound' ;
        } else {
          this.searchState = 'searching' ;
        }
      // Controllo Stato Richiesta
        this.reqState = 'loading';
        console.log('Request State:' + ' ' + this.reqState);
        this.checkStatus();
      } catch (error) {
        this.reqState = 'error';
        this.searchState = 'error';
        this.noResp = true;
        console.log('Request State Feed:' + ' ' + this.reqState);
      }
    },
    checkStatus() {
      if (this.movieArray.length > 0 ) {
        this.reqState = 'loading complete';
        console.log('Request State:' + ' ' + this.reqState);
      }
    }
  }
}
</script>

<style lang="scss">
@import './styles/general.scss';

#app {
 background-color: black;
}
</style>
