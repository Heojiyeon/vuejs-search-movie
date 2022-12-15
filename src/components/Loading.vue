<template>
  <div id="loading-image">
    <img src="loading.gif" alt="로딩 이미지" />
  </div>
</template>

<style lang="scss" scoped>
#loading-image {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translateX(-50%);
  width: 100px;
  height: 100px;
  z-index: 99999;
}
</style>
