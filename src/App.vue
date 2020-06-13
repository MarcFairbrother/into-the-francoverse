<template>
  <div id="app">
    <header>
      <h1>
        <span class="into">Into the</span>
        <br />
        <span class="francoverse">FrancoVerse</span>
      </h1>
      <h2>An Experiment in Data Visualisation</h2>
    </header>
    <FilmsMain />
  </div>
</template>

<script>
import FilmsMain from "./components/FilmsMain";

export default {
  name: "app",
  components: {
    FilmsMain
  }
};
</script>

<style lang="scss">
@import "./assets/styles/_globals.scss";
</style>