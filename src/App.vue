<template>
  <div id="app">
    <headerFlix @search="getDataMoviesAndSeries" />
    <mainFlix :listFilms="dataMovies" :listSeries='dataSeries'/>
    
  </div>
</template>

<script>
import axios from 'axios';

import headerFlix from './components/headerFlix.vue'
import mainFlix from './components/mainFlix.vue'

export default {
  data: function() {
    return{
      dataMovies: [],
      dataSeries: [],
      
      
    }

  },

  name: 'App',
  components: {
    mainFlix,
    headerFlix,
  },

  methods: {
    getDataMovies(search) {
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=76a0f6b38de7b73cfe6c7dd173889613&query=${search}`)
        .then((result) => {
          this.dataMovies = result.data.results;
          console.log(result.data.results);
        })
        .catch((error) => {
          console.log(error);
        })
    },

    getDataSeries(search) {
      axios.get(`https://api.themoviedb.org/3/search/tv?api_key=76a0f6b38de7b73cfe6c7dd173889613&query=${search}`)
        .then((result) => {
          this.dataSeries = result.data.results;
          console.log(result.data.results);
        })
        .catch((error) => {
          console.log(error);
        })
    },

    getDataMoviesAndSeries(search) {
      this.getDataMovies(search);
      this.getDataSeries(search);
    }

  },

  
}
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap.scss";
@import "./styles/general.scss";


</style>
