<template>
  <section class="intro">
    <article class="intro__content">
      <p>
        Between 1959 and 2013, Jess Franco directed nearly 200 films ranging
        from euro-westerns to cheapo skin flicks, and encompassing pretty much
        every other genre in between.
      </p>
      <p>
        He would frequently shoot multiple films at the same time, recycling his
        cast and locations to tell tales which obsessively explore themes of
        macabre lust through meandering narratives.
      </p>
      <p>He directed up to 13 films in a single year.</p>
      <p>
        This project is an attempt to make some sense of his compulsive
        film-making.
      </p>
    </article>
  </section>
</template>

<script>
export default {
  name: "SiteIntro"
};
</script>

<style lang="scss" scoped>
.intro {
  color: var(--dark-grey);
  @include breakpoint($desktop-width) {
    display: grid;
    grid-row: 2;
    grid-template-columns: repeat(12, 1fr);
    &::before {
      background: var(--dark-grey);
      display: block;
      content: "";
      grid-column: 10/11;
      grid-row: 1;
      height: 60px;
    }
    &::after {
      background: var(--dark-grey)
        url("data:image/svg+xml; utf8, %3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22100%22%20height%3D%2220%22%20viewBox%3D%220%200%2026.458332%205.291667%22%3E%0A%20%20%3Cg%20transform%3D%22translate%280%20-291.70832%29%22%20paint-order%3D%22fill%20markers%20stroke%22%3E%0A%20%20%20%20%3Ccircle%20cx%3D%222.6458333%22%20cy%3D%22294.35416%22%20r%3D%222.6458333%22%20fill%3D%22%2345b3b1%22%2F%3E%0A%20%20%20%20%3Ccircle%20r%3D%222.6458333%22%20cy%3D%22294.35416%22%20cx%3D%2213.229167%22%20fill%3D%22%23e48a99%22%2F%3E%0A%20%20%20%20%3Ccircle%20cx%3D%2223.8125%22%20cy%3D%22294.35416%22%20r%3D%222.6458333%22%20fill%3D%22%239c83c6%22%2F%3E%0A%20%20%3C%2Fg%3E%0A%3C%2Fsvg%3E");
      background-position: bottom 2rem left 5rem;
      background-repeat: no-repeat;
      background-size: 10rem;
      border-radius: 0 0 0 50px;
      content: "";
      grid-column: 11/13;
      grid-row: 1;
      margin-bottom: 1rem;
      transform: translateX(-1rem);
      width: calc(100% + 1rem);
    }
  }
  &__content {
    padding: 2rem;
    @include breakpoint($desktop-width) {
      background: var(--vintage-blue)
        url("../assets/img/stills/vampyros_lesbos_halftone.png");
      background-blend-mode: darken;
      background-position: center;
      background-size: cover;
      border: solid 1rem var(--off-white);
      border-left: none;
      border-radius: 0 50px 50px 0;
      clip-path: polygon(
        0 1rem,
        100px 1rem,
        100px 0,
        100% 0,
        100% 100%,
        0 100%
      );
      color: var(--off-white);
      display: grid;
      grid-template-columns: repeat(10, 1fr);
      grid-column: 1/11;
      grid-row: 1;
      margin-right: 1rem;
      padding: 6rem;
      @include breakpoint($large-width) {
        padding: 12rem 10rem;
      }
    }
    & > p {
      font-size: 2rem;
      grid-column: 1/11;
      line-height: 3rem;
      margin-bottom: 2rem;
      &:last-of-type {
        margin-bottom: 0;
      }
      @include breakpoint($desktop-width) {
        font-size: 3rem;
        font-weight: 400;
        grid-column: 6/11;
        line-height: 5rem;
        margin-bottom: 3rem;
        margin-left: 2rem;
        text-align: right;
        text-shadow: 0 0 4px var(--dark-grey);
      }
      @include breakpoint($large-width) {
        font-size: 4rem;
        line-height: 6rem;
        margin-left: 6rem;
        margin-bottom: 4rem;
      }
    }
  }
}
</style>