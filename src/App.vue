<template>
  <div id="app">
    <GifDisplay></GifDisplay>
  </div>
</template>

<script>
import Test from "./components/Test";
import GifDisplay from "./components/GifDisplay";
import Search from "./components/Search";

export default {
  name: "app",

  components: { Test, GifDisplay, Search },

  data() {
    return {};
  },
};
</script>

<style>
html {
  width: 100%;
  height: 100%;
}
body {
  height: 100%;
  width: 100%;
  margin: 0;
  background-image: linear-gradient(
    to top right,
    rgb(231, 125, 255),
    rgb(24, 10, 150)
  );
}

#app {
  height: 100%;
}
</style>
