<template>
  <form>
    <input
      id="search-bar"
      type="text"
      placeholder="검색할 영화 제목을 입력해주세요"
    />
    <button id="submit-btn" type="submit" @click="searchMovies">Search</button>
  </form>
</template>

<script>
export default {
  props: {
    searchKeyword: {
      type: String,
    },
  },
  methods: {
    searchMovies(e) {
      e.preventDefault();
      const currentKeyword = document.querySelector('input').value;
      if (currentKeyword.length < 1) {
        alert('정확한 정보를 입력해주세요!');
      }
      this.$emit('printMovies', currentKeyword);
    },
  },
};
</script>

<style lang="scss" scoped>
* {
  font-family: 'Roboto', sans-serif;
}
form {
  display: flex;
  margin: 10px;
}
#search-bar {
  width: 500px;
  font-size: 15px;
  margin-right: 10px;
  padding: 5px;
  padding-bottom: 2%;
  background-color: none;
}
#submit-btn {
  font-size: 15px;
  border-radius: 10px;
  border-style: none;
  background-color: none;
}
</style>
