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
      rgba(0, 0, 0, 0.25) -20%,
      rgba(0, 0, 0, 0) 40%,
      rgba(0, 0, 0, 0) 70%,
      rgba(0, 0, 0, 0.35) 120%
    ),
    var(--pulp-red);
  color: var(--pulp-beige);
  padding: 15px 15px 20px;
  & > h1 {
    font-family: "Changa One", Arial, Helvetica, sans-serif;
    font-variant: small-caps;
    margin-bottom: 20px;
    text-shadow: -3px 3px 0 rgb(10, 10, 10), -1px -1px 0 rgb(10, 10, 10),
      1px -1px 0 rgb(10, 10, 10), -1px 1px 0 rgb(10, 10, 10),
      1px 1px 0 rgb(10, 10, 10);
    transform: skew(-15deg, -10deg) rotate(5deg);
    & > span.into {
      font-size: 45px;
      letter-spacing: 3px;
    }
    & > span.francoverse {
      font-size: 70px;
      letter-spacing: 2px;
      margin-left: 15px;
    }
  }
  & > h2 {
    font-family: "Special Elite", Times, serif;
    font-size: 16px;
    margin-right: 10px;
    text-align: right;
    text-shadow: -1px -1px 0 rgb(10, 10, 10), 1px -1px 0 rgb(10, 10, 10),
      -1px 1px 0 rgb(10, 10, 10), 1px 1px 0 rgb(10, 10, 10);
  }
}
</style>