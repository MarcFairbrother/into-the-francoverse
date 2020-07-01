<template>
  <ul>
    <li class="film" v-for="(film, i) in selectedFilms" :key="i">
      <article class="film__card">
        <ul class="film__colors">
          <li
            v-for="(color, n) in film.colors"
            :key="n"
            :style="`background: ${color}`"
          ></li>
        </ul>
        <h4 class="film__title">{{ film.title }} ({{ film.year }})</h4>
        <ul class="film__tags">
          <li
            v-for="(filter, t) in film.filters"
            :key="t"
            :style="`--selection-color: ${filter.color}`"
          >
            {{ filter.type }}: {{ filter.value }}
          </li>
        </ul>
        <a
          :href="`https://www.imdb.com/title/${film.imdb}`"
          target="_blank"
          :title="`${film.title} on IMDb`"
          v-show="film.imdb.length > 0"
          class="film__imdb"
        >
          {{ film.title }} on IMDb
        </a>
      </article>
    </li>
  </ul>
</template>

<script>
export default {
  name: "FilmsList",
  props: ["filmSelections"],
  computed: {
    selectedFilms: function() {
      const data = [];
      this.filmSelections.forEach(selection => {
        selection.currentFilms.forEach(film => {
          const matchingTitle = data.find(item => item.title === film.title);
          if (matchingTitle) {
            // add selection color to matching film on films list
            matchingTitle.colors.push(Object.values(selection.color)[0]);
            // create new filter object and add to mathcing film
            this.addSelectedFilter(selection, matchingTitle);
          } else {
            // create new film object to add to films list
            const newFilm = {
              title: film.title,
              id: film.id,
              year: film.year,
              colors: [Object.values(selection.color)[0]],
              imdb: film.imdb,
              filters: []
            };
            // create new filter object and add to new film
            this.addSelectedFilter(selection, newFilm);
            // add new film object to films list
            data.push(newFilm);
          }
        });
      });
      // sort the array by film id and return the value
      return data.sort(function(a, b) {
        return a.id - b.id;
      });
    }
  },
  methods: {
    // creates a new object with a filter's values
    addSelectedFilter: function(data, target) {
      data.selectedFilters.forEach(filter => {
        for (const key in filter) {
          const newFilter = {
            type: key,
            value: filter[key],
            color: Object.values(data.color)[0]
          };
          target.filters.push(newFilter);
        }
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.film {
  background: var(--dark-grey);
  border-radius: 50px;
  &__card {
    background: url("data:image/svg+xml; utf8, %3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%2248%22%20height%3D%2248%22%20viewBox%3D%220%200%2012.7%2012.7%22%3E%3Cpath%20d%3D%22M8.467%2012.7V0h2.117v12.7zm-4.234%200V0H6.35v12.7zM0%2012.7V0h2.117v12.7z%22%20fill%3D%22%23f1f0e9%22%20paint-order%3D%22fill%20markers%20stroke%22%2F%3E%3C%2Fsvg%3E");
    background-position: right;
    background-repeat: repeat-y;
    background-size: 3rem;
    color: var(--off-white);
    height: 100%;
    padding: 4rem;
  }
  &__title {
    font-size: 2rem;
    line-height: 3rem;
    margin-bottom: 4rem;
  }
  &__colors {
    display: flex;
    margin-bottom: 4rem;
    & > li {
      border-radius: 50%;
      margin-right: 2rem;
      height: 2rem;
      width: 2rem;
    }
  }
  &__tags {
    display: flex;
    flex-wrap: wrap;
    & > li {
      align-items: center;
      border: solid 1px var(--off-white);
      border-radius: 2rem;
      display: flex;
      font-size: 1.5rem;
      font-weight: 400;
      line-height: 2rem;
      margin-bottom: 2rem;
      margin-right: 2rem;
      padding: 1rem 1rem;
      text-transform: capitalize;
      &::before {
        background: var(--selection-color);
        border-radius: 50%;
        content: "";
        display: block;
        height: 1rem;
        margin-right: 1rem;
        width: 1rem;
      }
    }
  }
  &__imdb {
    background: url("data:image/svg+xml; utf8, %3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20class%3D%22ipc-logo%22%20width%3D%2264%22%20height%3D%2232%22%3E%0A%20%20%3Cpath%20d%3D%22M4%200C1.784%200%200%201.784%200%204v24c0%202.216%201.784%204%204%204h56c2.216%200%204-1.784%204-4V4c0-2.216-1.784-4-4-4H4zm4%207h5v18H8V7zm7%200h6.277344c.185134%201.0917512.378487%202.3710046.580078%203.835938l.695312%204.572265L23.671875%207H30v18h-4.228516l-.013672-12.148438L24.0625%2025h-3.019531l-1.785157-11.886719L19.242188%2025H15V7zm17%200h7.804688C41.569481%207%2043%208.4191215%2043%2010.175781v11.648438C43%2023.578609%2041.57179%2025%2039.804688%2025H32V7zm13%200h4.785156v5.78125c.618172-.770379%201.569775-1.273438%202.644532-1.273438H52.75c1.795192%200%203.25%201.404527%203.25%203.136719v7.216797C56%2023.594402%2054.545664%2025%2052.75%2025h-.320312c-1.098447%200-2.069799-.526643-2.658204-1.332031l-.287109%201.101562H45V7zm-8.296875%203.080078v11.810547c.728633%200%201.175605-.130367%201.34375-.404297.168146-.26996.255859-1.000278.255859-2.199219v-6.978515c0-.813851-.029887-1.334193-.085937-1.564453-.05605-.23026-.18213-.396717-.384766-.503907-.198326-.10719-.577042-.160156-1.128906-.160156zm13.828125%204.208984c-.263906%200-.670829.111633-.75.298829v7.21875c.09048.205549.478554.320312.75.320312s.667058-.111093.75-.320312c.08294-.20922.125-.717643.125-1.521485v-4.265625c0-.704739-.046372-1.167969-.140625-1.380859-.09425-.21289-.470469-.349609-.734375-.34961z%22%20fill%3D%22%23f1f0e9%22%2F%3E%0A%3C%2Fsvg%3E");
    background-position: center;
    background-repeat: no-repeat;
    background-size: 100%;
    color: var(--off-white);
    display: inline-block;
    font-size: 0;
    height: 2.5rem;
    width: 5rem;
  }
}
</style>