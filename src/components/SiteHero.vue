<template>
  <section class="hero">
    <header class="hero__header">
      <h1 class="hero__title">Into the Franco Verse</h1>
      <SiteLogo class="hero__logo" />
      <p class="hero__description">An Experiment in Data Visualisation</p>
      <ul class="hero__hook">
        <li>Psychedelic Sadism</li>
        <li>Murderous Lust</li>
        <li>Ertica Exotica</li>
      </ul>
    </header>
    <ul class="hero__images">
      <li>Insert Image</li>
      <li>Insert Image</li>
      <li>Insert Image</li>
      <li>Insert Image</li>
      <li>Insert Image</li>
      <li>Insert Image</li>
    </ul>
  </section>
</template>

<style lang="scss" scoped>
.hero {
  display: grid;
  grid-template-columns: 1fr 1fr;
  height: 100vh;
  &__header {
    background: var(--dark-grey);
    color: var(--off-white);
    display: grid;
    grid-template-columns: 1fr;
    grid-column: 1;
  }
  &__title {
    font-size: 0;
    grid-row: 2;
  }
  &__logo {
    grid-row: 3;
    margin-right: calc(2 * var(--base-unit));
  }
  &__description {
    grid-row: 4;
    margin: calc(2 * var(--base-unit));
  }
  &__hook {
    display: flex;
    grid-row: 1;
    margin: calc(2 * var(--base-unit));
    & > li {
      font-size: 0;
      &::before {
        background: white;
        border-radius: 50%;
        content: "";
        display: inline-block;
        height: calc(2 * var(--base-unit));
        margin-right: calc(2 * var(--base-unit));
        width: calc(2 * var(--base-unit));
      }
    }
  }
  &__images {
    display: grid;
    grid-column: 2;
    grid-template-columns: 1fr;
  }
}
</style>

<script>
import SiteLogo from "./SiteLogo";

export default {
  name: "SiteHero",
  components: {
    SiteLogo
  }
};
</script>