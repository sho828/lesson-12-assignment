<script setup></script>

<template>
  <router-view />
  <!-- 変更 -->
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  color: #040000;
  line-height: 1;
  font-family: sans-serif;
}

body {
  position: absolute;
  height: 100%;
  width: 100%;
  background: rgb(255, 255, 255);
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: rgb(255, 255, 255);
  /* background: linear-gradient(
    180deg,
    rgba(255, 255, 255, 1) 0%,
    rgba(219, 219, 219, 1) 100%
  ); */
}
/* 
@media screen and (max-width: 540px) {
  body {
    touch-action: pan-x pan-y;
  }
} */
</style>
