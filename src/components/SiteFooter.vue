<template>
  <footer class="footer">
    <section class="footer__content">
      <p>This website is dedicated to Soledad, Lina, and Jess.</p>
      <p>
        The data is based on the filmography established by Stephen Thrower in
        <em>Murderous Passions</em> and <em>Flowers of Perversion</em>,
        respectively published by Strange Attractor in 2015 and 2019.
      </p>
      <p>Additional information was gleaned from IMDb when necessary.</p>
      <p class="legal">
        Source code hosted on
        <a
          href="https://github.com/MarcFairbrother/into-the-francoverse"
          target="_blank"
          >GitHub</a
        >
      </p>
      <p class="legal">Website hosted and deployed by Netlify</p>
      <p class="legal">
        Netlify, Inc.<br />2325 3RD STREET,SUITE 215, SAN FRANCISCO, CA 94107
        (USA)<br />privacy@netlify.com<br />www.netlify.com<br />+1 844-899-7312
      </p>
    </section>
    <section class="footer__copyright">
      <p>MarcFairbrother<span>&copy;</span>2020</p>
    </section>
  </footer>
</template>

<script>
export default {
  name: "SiteFooter"
};
</script>

<style lang="scss" scoped>
.footer {
  background: var(--dark-grey);
  color: var(--off-white);
  font-size: 2rem;
  font-weight: 400;
  line-height: 3rem;
  margin-top: 4rem;
  @include breakpoint($desktop-width) {
    display: grid;
    font-size: 3rem;
    grid-template-columns: repeat(12, 1fr);
    line-height: 5rem;
    margin-top: 6rem;
  }
  @include breakpoint($large-width) {
    font-size: 4rem;
    line-height: 6rem;
  }
  &::before {
    @include breakpoint($desktop-width) {
      border: solid 0.5rem var(--off-white);
      border-radius: 0 0 4rem 0;
      border-left: none;
      border-top: none;
      content: "";
      grid-column: 1;
      grid-row: 1;
      transform: translateX(-7.5rem);
    }
    @include breakpoint($large-width) {
      transform: translateX(-10.5rem);
    }
  }
  &::after {
    @include breakpoint($desktop-width) {
      border: double 1.5rem var(--off-white);
      border-radius: 0 0 6rem 0;
      border-left: none;
      border-top: none;
      content: "";
      grid-column: 1;
      grid-row: 1;
      transform: translateX(-5.5rem) translateY(2rem);
    }
    @include breakpoint($large-width) {
      transform: translateX(-8.5rem) translateY(2rem);
    }
  }
  & a {
    color: var(--off-white);
    text-decoration: underline;
  }
  &__content {
    border: solid 0.5rem var(--off-white);
    border-radius: 0 0 0 4rem;
    border-right: none;
    border-top: none;
    margin-left: 4.5rem;
    padding: 4rem 4rem 4rem 2rem;
    position: relative;
    @include breakpoint($desktop-width) {
      background: url("../assets/img/stills/female_vampire_halftone.png");
      background-position: center;
      background-size: cover;
      background-blend-mode: multiply;
      grid-column: 2/13;
      grid-row: 1;
      margin-left: 0;
      padding: 6rem 7rem;
      transform: translateX(-6rem);
      width: calc(100% + 6rem);
    }
    @include breakpoint($large-width) {
      padding: 15rem 9rem;
      transform: translateX(-9rem);
      width: calc(100% + 9rem);
    }
    &::before {
      border: double 1.5rem var(--off-white);
      border-radius: 0 0 0 6rem;
      border-right: none;
      border-top: none;
      bottom: -2.5rem;
      content: "";
      display: block;
      left: -2.5rem;
      position: absolute;
      pointer-events: none;
      right: 0;
      top: 0;
    }
    & p {
      margin-bottom: 1rem;
      &:last-of-type {
        margin-bottom: 0;
      }
      @include breakpoint($desktop-width) {
        margin-bottom: 3rem;
        width: 45%;
      }
      @include breakpoint($large-width) {
        margin-bottom: 4rem;
      }
      &.legal {
        font-size: 1.5rem;
        line-height: 2rem;
        @include breakpoint($desktop-width) {
          margin-bottom: 2rem;
        }
      }
    }
  }
  &__copyright {
    padding: 4rem 4rem 2rem 7rem;
    @include breakpoint($tablet-width) {
      display: flex;
      justify-content: space-between;
      &::after {
        background: url("data:image/svg+xml; utf8, %3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22100%22%20height%3D%2220%22%20viewBox%3D%220%200%2026.458332%205.291667%22%3E%0A%20%20%3Cg%20transform%3D%22translate%280%20-291.70832%29%22%20paint-order%3D%22fill%20markers%20stroke%22%3E%0A%20%20%20%20%3Ccircle%20cx%3D%222.6458333%22%20cy%3D%22294.35416%22%20r%3D%222.6458333%22%20fill%3D%22%231cbdba%22%2F%3E%0A%20%20%20%20%3Ccircle%20r%3D%222.6458333%22%20cy%3D%22294.35416%22%20cx%3D%2213.229167%22%20fill%3D%22%23f73636%22%2F%3E%0A%20%20%20%20%3Ccircle%20cx%3D%2223.8125%22%20cy%3D%22294.35416%22%20r%3D%222.6458333%22%20fill%3D%22%23f113cb%22%2F%3E%0A%20%20%3C%2Fg%3E%0A%3C%2Fsvg%3E");
        background-size: 10rem;
        content: "";
        display: block;
        height: 2rem;
        margin-top: 0;
        width: 10rem;
      }
    }
    @include breakpoint($desktop-width) {
      grid-column: 2/12;
      grid-row: 2;
      padding: 5rem 2rem 4rem 2rem;
      padding: 5rem 1rem 3rem;
    }
    @include breakpoint($large-width) {
      padding: 5rem 0 3rem;
    }
    & p {
      display: flex;
      font-size: 1.5rem;
      line-height: 2rem;
      @include mobile {
        &::before {
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
    & span {
      margin-left: 2px;
      margin-right: 1px;
      transform: rotate(180deg);
    }
  }
}
</style>