<template>
  <ul class="search-result-list">
    <li class="search-result-movie" v-for="movie in movies" :key="movie.imdbID">
      <Modal>
        <template #activator>
          <img
            class="movie-poster"
            @click="sendMovieId(movie.imdbID)"
            :src="movie.Poster"
            alt="영화 포스터 이미지"
        /></template>

        <template #content>
          <div id="movie-poster">
            <img :src="targetMovieDetail.Poster" alt="" />
          </div>
          <div id="movie-title">Title: {{ targetMovieDetail.Title }}</div>
          <br />
          <div id="movie-release-date">
            Release date: {{ targetMovieDetail.Released }}
          </div>
          <br />
          <div id="movie-running-time">
            Running time: {{ targetMovieDetail.Runtime }}
          </div>
          <br />
          <div id="movie-director">
            Director: {{ targetMovieDetail.Director }}
          </div>
          <br />
          <div id="movie-plot">Plot: {{ targetMovieDetail.Plot }}</div>
        </template>
      </Modal>
    </li>
  </ul>
</template>

<script>
import Modal from '~/components/Modal';
export default {
  props: {
    movies: {
      type: Object,
    },
    targetMovieId: {
      type: String,
    },
    targetMovieDetail: {
      type: Object,
    },
  },
  components: {
    Modal,
  },
  methods: {
    sendMovieId(currId) {
      this.$emit('showMovieDetail', currId);
    },
  },
};
</script>

<style lang="scss" scoped>
* {
  font-family: 'Roboto', sans-serif;
}
.search-result-movie {
  margin: 10px;
  list-style: none;
}
</style>
