<template>
  <ul>
    <li class="film" v-for="(film, i) in selectedFilms" :key="i">
      <a
        :href="`https://www.imdb.com/title/${film.imdb}`"
        target="_blank"
        :title="`${film.title} on IMDb`"
      >
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
        </article>
      </a>
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
}
</style>