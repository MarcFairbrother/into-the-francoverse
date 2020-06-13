<template>
  <div id="app">
    <SiteHero />
    <SiteIntro />
    <FilmsMain />
  </div>
</template>

<script>
import SiteHero from "./components/SiteHero";
import SiteIntro from "./components/SiteIntro";
import FilmsMain from "./components/FilmsMain";

export default {
  name: "app",
  components: {
    SiteHero,
    SiteIntro,
    FilmsMain
  }
};
</script>

<style lang="scss">
@import "./assets/styles/_globals.scss";
</style>