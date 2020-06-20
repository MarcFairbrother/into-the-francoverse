<template>
  <div id="app" class="wrapper">
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
@include breakpoint($desktop-width) {
  .wrapper {
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    grid-auto-rows: auto;
    &::before {
      border-top: solid 0.5rem var(--off-white);
      border-right: solid 0.5rem var(--off-white);
      border-radius: 0 56px 0 0;
      content: "";
      display: block;
      grid-column: 1/11;
      grid-row: 2;
      height: 100%;
      transform: translateX(4rem) translateY(-1rem);
      width: calc(100% - 4.5rem);
      z-index: 15;
    }
    &::after {
      border-top: double 1.5rem var(--off-white);
      border-right: double 1.5rem var(--off-white);
      border-radius: 0 70px 0 0;
      content: "";
      display: block;
      grid-column: 1/11;
      grid-row: 2;
      height: 100%;
      transform: translateX(2.5rem) translateY(-3rem);
      width: calc(100% - 2rem);
      z-index: 15;
    }
    & > * {
      grid-column: 1/13;
    }
  }
}
</style>