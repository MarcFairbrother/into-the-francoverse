<template>
  <div id="app" class="wrapper">
    <SiteHero />
    <SiteIntro />
    <FilmsMain />
    <SiteFooter />
  </div>
</template>

<script>
import SiteHero from "./components/SiteHero";
import SiteIntro from "./components/SiteIntro";
import FilmsMain from "./components/FilmsMain";
import SiteFooter from "./components/SiteFooter";

export default {
  name: "app",
  components: {
    SiteHero,
    SiteIntro,
    FilmsMain,
    SiteFooter
  }
};
</script>

<style lang="scss">
@import "./assets/styles/_globals.scss";
.wrapper {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: auto;
  @include breakpoint($desktop-width) {
    grid-template-columns: repeat(12, 1fr);
  }
  &::before {
    align-self: end;
    border-top: solid 0.5rem var(--off-white);
    border-right: solid 0.5rem var(--off-white);
    border-radius: 0 56px 0 0;
    content: "";
    display: block;
    grid-column: 1/4;
    grid-row: 2;
    height: calc(100% - 4.5rem);
    width: calc(100% + 0.5rem);
    z-index: 15;
    @include breakpoint($tablet-width) {
      height: calc(100% - 8.5rem);
    }
    @include breakpoint($desktop-width) {
      align-self: start;
      grid-column: 1/11;
      height: 100%;
      transform: translateX(4rem) translateY(-1rem);
      width: calc(100% - 4.5rem);
    }
  }
  &::after {
    align-self: end;
    border-top: double 1.5rem var(--off-white);
    border-right: double 1.5rem var(--off-white);
    border-radius: 0 70px 0 0;
    content: "";
    display: block;
    grid-column: 1/4;
    grid-row: 2;
    height: calc(100% - 3.5rem);
    width: calc(100% + 1.5rem);
    z-index: 15;
    @include breakpoint($tablet-width) {
      height: calc(100% - 7.5rem);
    }
    @include breakpoint($desktop-width) {
      align-self: start;
      grid-column: 1/11;
      height: 100%;
      transform: translateX(2.5rem) translateY(-3rem);
      width: calc(100% - 2rem);
    }
  }
  & > * {
    grid-column: 1/5;
  }
  @include breakpoint($desktop-width) {
    & > * {
      grid-column: 1/13;
    }
  }
}
</style>