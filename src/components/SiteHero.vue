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
        <picture class="blue-tint">
          <source
            srcset="../assets/img/stills/she_killed_in_ecstasy_soledad_desk.jpg"
            media="(min-width: 1024px)"
          />
          <source
            srcset="../assets/img/stills/she_killed_in_ecstasy_soledad_tablet.jpg"
            media="(min-width: 768px)"
          />
          <source
            srcset="../assets/img/stills/she_killed_in_ecstasy_soledad_mobile.jpg"
            media="(max-width: 767px)"
          />
          <img
            src="../assets/img/stills/she_killed_in_ecstasy_soledad_mobile.jpg"
            alt="Soledad Miranda in She Killed in Ecstasy"
          />
        </picture>
      </li>
      <li data-slide="2" class="fade-out">
        <picture>
          <source
            srcset="../assets/img/stills/diabolical_dr_z_desk.jpg"
            media="(min-width: 1024px)"
          />
          <source
            srcset="../assets/img/stills/diabolical_dr_z_tablet.jpg"
            media="(min-width: 768px)"
          />
          <source
            srcset="../assets/img/stills/diabolical_dr_z_mobile.jpg"
            media="(max-width: 767px)"
          />
          <img
            src="../assets/img/stills/diabolical_dr_z_mobile.jpg"
            alt="Miss Muerte in The Diabolical Dr Z"
          />
        </picture>
      </li>
      <li data-slide="3" class="fade-out">
        <picture class="red-tint">
          <source
            srcset="../assets/img/stills/female_vampire_desk.jpg"
            media="(min-width: 1024px)"
          />
          <source
            srcset="../assets/img/stills/female_vampire_tablet.jpg"
            media="(min-width: 768px)"
          />
          <source
            srcset="../assets/img/stills/female_vampire_mobile.jpg"
            media="(max-width: 767px)"
          />
          <img
            src="../assets/img/stills/female_vampire_mobile.jpg"
            alt="Lina Romay in Female Vampire"
          />
        </picture>
      </li>
      <li data-slide="4" class="fade-out">
        <picture>
          <source
            srcset="../assets/img/stills/she_killed_in_ecstasy_desk.jpg"
            media="(min-width: 1024px)"
          />
          <source
            srcset="../assets/img/stills/she_killed_in_ecstasy_tablet.jpg"
            media="(min-width: 768px)"
          />
          <source
            srcset="../assets/img/stills/she_killed_in_ecstasy_mobile.jpg"
            media="(max-width: 767px)"
          />
          <img
            src="../assets/img/stills/she_killed_in_ecstasy_mobile.jpg"
            alt="She Killed in Ecstasy"
          />
        </picture>
      </li>
      <li data-slide="5" class="fade-out">
        <picture class="purple-tint">
          <source
            srcset="../assets/img/stills/countesse_perverse_desk.jpg"
            media="(min-width: 1024px)"
          />
          <source
            srcset="../assets/img/stills/countesse_perverse_tablet.jpg"
            media="(min-width: 768px)"
          />
          <source
            srcset="../assets/img/stills/countesse_perverse_mobile.jpg"
            media="(max-width: 767px)"
          />
          <img
            src="../assets/img/stills/countesse_perverse_mobile.jpg"
            alt="Alie Arno in Countesse Perverse"
          />
        </picture>
      </li>
      <li data-slide="6" class="fade-out">
        <picture>
          <source
            srcset="../assets/img/stills/sadist_of_notre_dame_desk.jpg"
            media="(min-width: 1024px)"
          />
          <source
            srcset="../assets/img/stills/sadist_of_notre_dame_tablet.jpg"
            media="(min-width: 768px)"
          />
          <source
            srcset="../assets/img/stills/sadist_of_notre_dame_mobile.jpg"
            media="(max-width: 767px)"
          />
          <img
            src="../assets/img/stills/sadist_of_notre_dame_mobile.jpg"
            alt="Jess Franco in The Sadist of Notre Dame"
          />
        </picture>
      </li>
    </ul>
  </section>
</template>

<style lang="scss" scoped>
.hero {
  background: var(--dark-grey);
  display: grid;
  grid-template-columns: 1fr 1fr;
  height: 100vh;
  @include breakpoint($tablet-width) {
    grid-template-columns: 1fr 2fr;
  }
  @include breakpoint($desktop-width) {
    background: none;
    grid-template-columns: 1fr 3fr;
    grid-template-rows: 86rem auto;
    height: 112rem;
    &::before {
      background: var(--vintage-blue)
        url("../assets/img/stills/halftone_pattern.png");
      background-blend-mode: darken;
      background-size: 150px;
      content: "";
      grid-column: 1;
      grid-row: 1/3;
      height: calc(100% - 1rem);
      margin-top: 2rem;
      width: 100px;
      z-index: 5;
      @include breakpoint($large-width) {
        background-size: 220px;
      }
      @include breakpoint($very-large) {
        background-size: 200px;
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
    grid-column: 1;
    grid-gap: 2rem;
    grid-template-columns: 1fr;
    grid-template-rows: repeat(8, 1fr);
    padding: 0;
    @include breakpoint($desktop-width) {
      border-bottom: solid 1rem var(--off-white);
      border-left: solid 1rem var(--off-white);
      grid-row: 1/3;
      height: calc(100% - 1rem);
      margin-left: 1rem;
      margin-top: 2rem;
      border-radius: 0 0 0 50px;
      overflow: visible;
      z-index: 5;
    }
  }
  &__title {
    font-size: 0;
    grid-column: 1;
    grid-row: 4/7;
  }
  &__logo {
    grid-column: 1;
    grid-row: 4/7;
    margin-right: 2rem;
    @include breakpoint($tablet-width) {
      align-self: end;
      transform: translateY(20%);
    }
    @include breakpoint($large-width) {
      width: 75%;
      margin-right: 0;
    }
  }
  &__description {
    align-self: end;
    font-size: 2rem;
    grid-row: 7/9;
    line-height: 2.5rem;
    margin: 0 2rem;
    text-align: left;
    @include breakpoint($tablet-width) {
      display: flex;
      line-height: 2rem;
      transform: translateY(4rem);
      width: 150%;
    }
    @include breakpoint($desktop-width) {
      align-items: center;
      flex-direction: row;
      font-size: 2rem;
      margin-bottom: 5rem;
      transform: translateY(0);
    }
    &::before {
      @include breakpoint($tablet-width) {
        background: url("data:image/svg+xml; utf8, %3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22100%22%20height%3D%2220%22%20viewBox%3D%220%200%2026.458332%205.291667%22%3E%0A%20%20%3Cg%20transform%3D%22translate%280%20-291.70832%29%22%20paint-order%3D%22fill%20markers%20stroke%22%3E%0A%20%20%20%20%3Ccircle%20cx%3D%222.6458333%22%20cy%3D%22294.35416%22%20r%3D%222.6458333%22%20fill%3D%22%2345b3b1%22%2F%3E%0A%20%20%20%20%3Ccircle%20r%3D%222.6458333%22%20cy%3D%22294.35416%22%20cx%3D%2213.229167%22%20fill%3D%22%23e48a99%22%2F%3E%0A%20%20%20%20%3Ccircle%20cx%3D%2223.8125%22%20cy%3D%22294.35416%22%20r%3D%222.6458333%22%20fill%3D%22%239c83c6%22%2F%3E%0A%20%20%3C%2Fg%3E%0A%3C%2Fsvg%3E");
        background-size: 10rem;
        content: "";
        display: block;
        height: 2rem;
        margin-top: 0;
        margin-right: 2rem;
        width: 10rem;
      }
    }
  }
  &__hook {
    display: flex;
    grid-row: 1/4;
    margin: calc(2rem + 2px) 2rem 0;
    @include breakpoint($tablet-width) {
      flex-direction: column;
    }
    & > li {
      font-size: 0;
      @include breakpoint($tablet-width) {
        align-items: center;
        display: flex;
        font-size: 2rem;
        line-height: 1.5rem;
        margin-bottom: 2rem;
      }
      &:nth-of-type(1):before {
        background: #45b3b1;
      }
      &:nth-of-type(2):before {
        background: #e48a99;
      }
      &:nth-of-type(3):before {
        background: #9c83c6;
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
    border-radius: 0 0 0 48px;
    display: grid;
    grid-column: 2;
    grid-template-columns: 1fr;
    overflow: hidden;
    @include breakpoint($tablet-width) {
      background: var(--off-white);
      grid-template-columns: repeat(6, 1fr);
      grid-template-rows: repeat(8, 1fr);
      grid-gap: 2rem;
      padding: 2rem;
    }
    @include breakpoint($desktop-width) {
      border-radius: 0;
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
          & img {
            border-radius: 0 40px 0 0;
          }
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
          & img {
            border-radius: 0 0 0 40px;
          }
        }
        &:nth-of-type(1) {
          grid-column: 4/7;
          grid-row: 6/9;
        }
      }
      @include breakpoint($desktop-width) {
        &:nth-of-type(4) {
          & img {
            border-radius: 0;
          }
        }
        &:nth-of-type(3) {
          grid-column: 3/8;
          grid-row: 3/5;
          margin-top: 6rem;
        }
        &:nth-of-type(6) {
          grid-column: 1/4;
          grid-row: 5/7;
        }
        &:nth-of-type(2) {
          grid-column: 4/7;
          grid-row: 5/7;
          & img {
            border-radius: 0;
          }
        }
        &:nth-of-type(1) {
          grid-column: 7/10;
          grid-row: 1/7;
          & img {
            border-radius: 0 50px 0 0;
          }
        }
      }
      & > picture,
      & img {
        display: block;
        height: 100%;
        object-fit: cover;
        width: 100%;
        &.blue-tint {
          filter: sepia(100%) hue-rotate(130deg) saturate(225%);
        }
        &.red-tint {
          filter: sepia(100%) hue-rotate(300deg) saturate(175%);
        }
        &.purple-tint {
          filter: sepia(100%) hue-rotate(220deg) saturate(150%) brightness(80%)
            contrast(110%);
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