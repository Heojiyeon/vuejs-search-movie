<template>
  <header>
    <h1 id="header-title">Search any movie title!</h1>
    <div class="header-main">
      <SearchBar
        id="search-bar"
        :searchKeyword="searchKeyword"
        @printMovies="printMovies"
      />
    </div>
  </header>
  <div id="result-section" v-if="isInit">
    검색된 영화가 존재하지 않습니다 :(
  </div>
  <SearchResult
    id="search-result"
    :movies="movies"
    :targetMovieDetail="targetMovieDetail"
    @showMovieDetail="showMovieDetail"
  />

  <Loading v-if="isLoading" />
</template>

<script>
import { API_KEY } from '~/utils/url.js';
import SearchBar from '~/components/Search-bar';
import SearchResult from '~/components/Search-result';
import Modal from '~/components/Modal';
import Loading from '~/components/Loading';

export default {
  components: {
    SearchBar,
    SearchResult,
    Modal,
    Loading,
  },
  data() {
    return {
      searchKeyword: '',
      targetMovieId: '',
      targetMovieDetail: {},
      movies: [],
      isLoading: false,
      isInit: true,
    };
  },
  methods: {
    printMovies(currKeyword) {
      this.isLoading = true;
      this.isInit = false;
      this.searchKeyword = currKeyword;
      fetch(`https://www.omdbapi.com?apikey=${API_KEY}&s=${this.searchKeyword}`)
        .then((res) => res.json())
        .then((result) => {
          this.movies = result.Search;
          this.isLoading = false;
        });
    },
    showMovieDetail(currId) {
      this.isLoading = true;
      this.targetMovieDetail = {};
      fetch(`https://www.omdbapi.com?apikey=${API_KEY}&i=${currId}&plot=full`)
        .then((res) => res.json())
        .then((result) => {
          this.targetMovieDetail = result;
          this.isLoading = false;
        });
    },
  },
};
</script>

<style lang="scss" scoped>
* {
  font-family: 'Roboto', sans-serif;
}
header {
  background-color: #716f81;
  #header-title {
    width: fit-content;
    margin-left: 40%;
    padding-top: 2%;
  }
  .header-main {
    display: flex;
    justify-content: center;
  }
}
#result-section {
  font-size: 20px;
  position: absolute;
  margin: 200px 0 200px 0;
  left: 40%;
}
#search-result {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-content: center;
}
</style>
