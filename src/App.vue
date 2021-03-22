<template>
  <div id="app">
    <div class="container">
      <connection></connection>
      <div class="quran__app">
        <img class="quran-logo" src="./assets/quran.png" />
        <top-btn></top-btn>
        <play-list></play-list>
      </div>
    </div>
  </div>
</template>
<script>
import PlayList from "./components/playList.vue";
import topBtn from "./components/topBtn";
import connection from "./components/connectionMsg";
export default {
  components: {
    PlayList,
    topBtn,
    connection
  }
};
</script>
