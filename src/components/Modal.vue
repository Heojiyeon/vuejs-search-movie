<template>
  <div @click="onModal">
    <slot name="activator"> </slot>
  </div>
  <template v-if="isShow">
    <div class="modal" @click="offModal">
      <div
        :style="{ width: `${parseInt(width, 10)}px` }"
        class="modal__inner"
        @click.stop
      >
        <slot name="content"></slot>
      </div>
    </div>
  </template>
</template>

<script>
export default {
  props: {
    width: {
      type: [String, Number],
      default: 400,
    },
    targetMovieId: {
      type: String,
    },
    targetMovieDeatil: {
      type: Object,
    },
  },
  data() {
    return {
      isShow: false,
    };
  },
  methods: {
    onModal() {
      this.isShow = !this.isShow;
    },
    offModal() {
      this.isShow = !this.isShow;
    },
  },
};
</script>

<style lang="scss" scoped>
* {
  font-family: 'Roboto', sans-serif;
}
.modal {
  background-color: rgba(black, 0.5);
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 9;
  display: flex;
  justify-content: center;
  align-items: center;
  &__inner {
    background-color: white;
    box-sizing: border-box;
    width: 400px;
    height: 800px;
    overflow: scroll;
    padding: 20px;
    margin-left: 20px;
    #movie-poster {
      margin-left: 10px;
    }
  }
}
</style>
