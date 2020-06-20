<template>
  <section class="hero">
    <header class="hero__header">
      <h1 class="hero__title">Into the Franco Verse</h1>
      <SiteLogo class="hero__logo" />
      <p class="hero__description">An Experiment in Data Visualisation</p>
      <ul class="hero__hook">
        <li>Psychedelic Sadism</li>
        <li>Murderous Lust</li>
        <li>Erotica Exotica</li>
      </ul>
    </header>
    <ul class="hero__images">
      <li data-slide="1" class="fade-in">
        <img
          src="../assets/img/stills/she_killed_in_ecstasy_soledad_360_640.jpg"
          alt="Soledad Miranda in She Killed in Ecstasy"
          class="blue-tint"
        />
      </li>
      <li data-slide="2" class="fade-out">
        <img
          src="../assets/img/stills/diabolical_dr_z_360_640.jpg"
          alt="Miss Muerte in The Diabolical Dr Z"
        />
      </li>
      <li data-slide="3" class="fade-out">
        <img
          src="../assets/img/stills/female_vampire_360_640.jpg"
          alt="Lina Romay in Female Vampire"
          class="red-tint"
        />
      </li>
      <li data-slide="4" class="fade-out">
        <img
          src="../assets/img/stills/she_killed_in_ecstasy_360_640.jpg"
          alt="She Killed in Ecstasy"
        />
      </li>
      <li data-slide="5" class="fade-out">
        <img
          src="../assets/img/stills/countesse_perverse_360_640.jpg"
          alt="Alie Arno in Countesse Perverse"
          class="purple-tint"
        />
      </li>
      <li data-slide="6" class="fade-out">
        <img
          src="../assets/img/stills/sadist_of_notre_dame_360_640.jpg"
          alt="Jess Franco in The Sadist of Notre Dame"
        />
      </li>
    </ul>
  </section>
</template>

<style lang="scss" scoped>
.hero {
  display: grid;
  grid-template-columns: 1fr 1fr;
  height: 100vh;
  @include breakpoint($tablet-width) {
    grid-template-columns: 1fr 2fr;
  }
  @include breakpoint($desktop-width) {
    grid-template-columns: 1fr 3fr;
    grid-template-rows: max-content auto;
    height: 112rem;
    &::before {
      background: var(--vintage-blue)
        url("../assets/img/stills/halftone_pattern.png");
      background-blend-mode: darken;
      background-size: 150px;
      content: "";
      grid-column: 1;
      grid-row: 1/3;
      height: calc(100% + 1rem);
      margin-top: 2rem;
      width: 100px;
      @include breakpoint($large-width) {
        background-size: 220px;
      }
    }
    &::after {
      background: var(--dark-grey);
      content: "";
      grid-column: 2;
      grid-row: 2;
    }
  }
  &__header {
    background: var(--dark-grey);
    color: var(--off-white);
    display: grid;
    grid-template-columns: 1fr;
    grid-column: 1;
    @include breakpoint($desktop-width) {
      border-bottom: solid 1rem var(--off-white);
      border-left: solid 1rem var(--off-white);
      grid-row: 1/3;
      height: calc(100% - 1rem);
      margin-left: 1rem;
      margin-top: 2rem;
      border-radius: 0 0 0 50px;
    }
  }
  &__title {
    font-size: 0;
    grid-row: 2;
  }
  &__logo {
    grid-row: 3;
    margin-right: 2rem;
  }
  &__description {
    grid-row: 4;
    margin: 2rem;
  }
  &__hook {
    display: flex;
    grid-row: 1;
    margin: 2rem;
    @include breakpoint($tablet-width) {
      flex-direction: column;
    }
    & > li {
      font-size: 0;
      @include breakpoint($tablet-width) {
        align-items: center;
        display: flex;
        font-size: 2rem;
        line-height: 2rem;
        margin-bottom: 2rem;
      }
      &::before {
        background: white;
        border-radius: 50%;
        content: "";
        display: inline-block;
        height: 2rem;
        margin-right: 2rem;
        width: 2rem;
        @include breakpoint($tablet-width) {
          margin-top: -2px;
        }
      }
    }
  }
  &__images {
    display: grid;
    grid-column: 2;
    grid-template-columns: 1fr;
    overflow: hidden;
    @include breakpoint($tablet-width) {
      grid-template-columns: repeat(6, 1fr);
      grid-template-rows: repeat(8, 1fr);
      grid-gap: 2rem;
      padding: 2rem;
    }
    @include breakpoint($desktop-width) {
      grid-row: 1;
      grid-template-columns: repeat(9, 1fr);
      grid-template-rows: repeat(6, 12rem);
    }
    & li {
      @include mobile {
        grid-column: 1;
        grid-row: 1;
        width: 100vw;
        transition: opacity 1.75s ease-in-out, transform 3.5s ease-in-out;
        &.fade-in {
          opacity: 1;
        }
        &.fade-out {
          opacity: 0;
          transform: translateX(-50%);
        }
      }
      @include breakpoint($tablet-width) {
        &:nth-of-type(5) {
          grid-column: 1/4;
          grid-row: 1/5;
        }
        &:nth-of-type(4) {
          grid-column: 4/7;
          grid-row: 1/4;
        }
        &:nth-of-type(3) {
          grid-column: 3/7;
          grid-row: 4/6;
          position: relative;
          z-index: 5;
          &::before {
            background: var(--off-white);
            bottom: -2rem;
            content: "";
            left: -2rem;
            position: absolute;
            right: -2rem;
            top: -2rem;
          }
        }
        &:nth-of-type(6) {
          grid-column: 1/4;
          grid-row: 5/7;
        }
        &:nth-of-type(2) {
          grid-column: 1/4;
          grid-row: 7/9;
        }
        &:nth-of-type(1) {
          grid-column: 4/7;
          grid-row: 6/9;
        }
      }
      @include breakpoint($desktop-width) {
        &:nth-of-type(3) {
          grid-column: 3/8;
          grid-row: 3/5;
        }
        &:nth-of-type(6) {
          grid-column: 1/4;
          grid-row: 5/7;
        }
        &:nth-of-type(2) {
          grid-column: 4/7;
          grid-row: 5/7;
        }
        &:nth-of-type(1) {
          grid-column: 7/10;
          grid-row: 1/7;
        }
      }
      @include breakpoint($large-width) {
        &:nth-of-type(3) {
          grid-row: 3/5;
          margin-top: 6rem;
        }
      }
      & > img {
        display: block;
        height: 100%;
        object-fit: cover;
        width: 100%;
        &.blue-tint {
          filter: sepia(100%) hue-rotate(130deg) saturate(150%);
        }
        &.red-tint {
          filter: sepia(100%) hue-rotate(300deg) saturate(175%);
        }
        &.purple-tint {
          filter: sepia(100%) hue-rotate(220deg) saturate(125%);
        }
      }
    }
  }
}
</style>

<script>
import SiteLogo from "./SiteLogo";

export default {
  name: "SiteHero",
  components: {
    SiteLogo
  },
  mounted: function() {
    let i = 1;
    window.setInterval(() => {
      if (i < 6) {
        document
          .querySelector(`[data-slide="${i}"]`)
          .classList.replace("fade-in", "fade-out");
        document
          .querySelector(`[data-slide="${i + 1}"]`)
          .classList.replace("fade-out", "fade-in");
      } else {
        document
          .querySelector(`[data-slide="${i}"]`)
          .classList.replace("fade-in", "fade-out");
        document
          .querySelector(`[data-slide="1"]`)
          .classList.replace("fade-out", "fade-in");
      }
      if (i === 6) {
        i = 1;
      } else {
        i++;
      }
    }, 4000);
  }
};
</script>