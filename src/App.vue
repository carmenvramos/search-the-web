<template>
  <div id="app">
    <Loading :loading="loading"/>
    <SearchControl :onSearch="handleSearch"/>
    <NewsList :newslist="newslist"/>
  </div>
</template>

<script>
import SearchControl from './components/SearchControl';
import NewsList from './components/NewsList';
import Loading from './components/Loading';
import { getNews } from './services/api'; 

// eslint-disable-next-line
console.log(process.env.VUE_APP_API_KEY);

export default {
  data() {
    return {
      newslist: null,
      loading: false
    };
  },
  components: {
    NewsList,
    SearchControl,
    Loading
  },
  methods: {
    handleSearch(name) {
      this.loading = true;

      getNews(name).then(data => {
        this.newslist = data.articles;
        this.loading = false;
      });
    }
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
  position: relative;
}
</style>
