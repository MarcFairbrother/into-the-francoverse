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
    overflow: hidden;
    & li {
      grid-column: 1;
      grid-row: 1;
      width: 100vw;
      @include mobile {
        transition: opacity 1.75s ease-in-out, transform 3.5s ease-in-out;
        &.fade-in {
          opacity: 1;
        }
        &.fade-out {
          opacity: 0;
          transform: translateX(-50%);
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