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
    <Films />
  </div>
</template>

<script>
import Films from "./components/Films";

export default {
  name: "app",
  components: {
    Films
  }
};
</script>

<style lang="scss">
/* Site Header */
header {
  background: url("./assets/img/tear_01.png") top left repeat-x,
    url("./assets/img/tear_02.png") top right repeat-y,
    url("./assets/img/tear_03.png") bottom left repeat-x,
    url("./assets/img/tear_04.png") top left repeat-y,
    url("./assets/img/texture_01.png"),
    linear-gradient(
      0.48turn,
      rgba(0, 0, 0, 0.35) -20%,
      rgba(0, 0, 0, 0) 40%,
      rgba(0, 0, 0, 0) 70%,
      rgba(0, 0, 0, 0.35) 120%
    ),
    var(--pulp-red);
  color: var(--pulp-beige);
  display: grid;
  grid-template-columns: 1fr max-content 1fr;
  padding: 15px 15px 20px;
  @include breakpoint($tablet-width) {
    padding: 15px 15px 25px;
  }
  & > h1 {
    font-family: "Changa One", Arial, Helvetica, sans-serif;
    font-variant: small-caps;
    grid-column: 2;
    grid-row: 1;
    margin-bottom: 20px;
    text-shadow: -3px 3px 0 var(--dark-grey), -1px -1px 0 var(--dark-grey),
      1px -1px 0 var(--dark-grey), -1px 1px 0 var(--dark-grey),
      1px 1px 0 var(--dark-grey);
    transform: skew(-15deg, -10deg) rotate(5deg);
    @include breakpoint($tablet-width) {
      line-height: 0.9;
      margin-bottom: 30px;
      text-shadow: -5px 5px 0 var(--dark-grey), -1px -1px 0 var(--dark-grey),
        1px -1px 0 var(--dark-grey), -1px 1px 0 var(--dark-grey),
        1px 1px 0 var(--dark-grey);
    }
    @include breakpoint($desktop-width) {
      line-height: 0.8;
      text-shadow: -7px 7px 0 var(--dark-grey), -1px -1px 0 var(--dark-grey),
        1px -1px 0 var(--dark-grey), -1px 1px 0 var(--dark-grey),
        1px 1px 0 var(--dark-grey);
    }
    & > span.into {
      font-size: 45px;
      letter-spacing: 3px;
      @include breakpoint($tablet-width) {
        font-size: 90px;
        letter-spacing: 4px;
      }
      @include breakpoint($desktop-width) {
        font-size: 120px;
      }
      @include breakpoint($large-width) {
        font-size: 150px;
      }
    }
    & > span.francoverse {
      font-size: 70px;
      letter-spacing: 2px;
      margin-left: 15px;
      @include breakpoint($tablet-width) {
        font-size: 130px;
        letter-spacing: 4px;
      }
      @include breakpoint($desktop-width) {
        font-size: 180px;
      }
      @include breakpoint($large-width) {
        font-size: 200px;
      }
    }
  }
  & > h2 {
    font-family: "Special Elite", Times, serif;
    font-size: 16px;
    grid-column: 2;
    grid-row: 2;
    margin-right: 10px;
    text-align: right;
    text-shadow: -1px -1px 0 var(--dark-grey), 1px -1px 0 var(--dark-grey),
      -1px 1px 0 var(--dark-grey), 1px 1px 0 var(--dark-grey);
    @include breakpoint($tablet-width) {
      font-size: 20px;
    }
    @include breakpoint($large-width) {
      font-size: 24px;
    }
  }
}
</style>