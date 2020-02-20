<template>
  <div id="app">
    <search v-on:SearchRequested="handleSearch"></search>
    <p v-if="isLoading">Loading</p>
    <preview :gifs=gifs></preview>
  </div>
</template>

<script>
import Search from './components/Search.vue'
import Preview from './components/Preview.vue'
export default {
  name: 'app',
  components: { Search, Preview },
  data() {
    return {
      isLoading: true,
      gifs: []
    }
  },
  methods: {
    handleSearch(query) {
      this.gifs = [];
      this.isLoading = true;
      fetch(`http://api.giphy.com/v1/gifs/search?q=${query}&api_key=TA8rxKfpqFH7Pm8Cf7O8oApzLZvTzjMM`)
      .then((res) => { return res.json() })
      .then((res) => { 
        this.gifs = res.data; 
        this.isLoading = false;
      })
    }
  },
  created() {
    fetch('http://api.giphy.com/v1/gifs/trending?api_key=TA8rxKfpqFH7Pm8Cf7O8oApzLZvTzjMM')
    .then((res) => { return res.json() })
    .then((res) => { 
      this.gifs = res.data; 
      this.isLoading = false;
      })
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>