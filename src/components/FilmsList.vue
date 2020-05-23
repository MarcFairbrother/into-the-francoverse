<template>
  <ul>
    <li v-for="(film, i) in selectedFilms" :key="i">
      <h4>{{ film.title }} ({{ film.year }})</h4>
      <p v-for="(color, n) in film.colors" :key="n">{{ color }}</p>
      <ul>
        <li
          v-for="(filter, t) in film.filters"
          :key="t"
          :style="`background: ${filter.color}`"
        >
          {{ filter.type }}: {{ filter.value }}
        </li>
      </ul>
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
              year: film.year,
              colors: [Object.values(selection.color)[0]],
              filters: []
            };
            // create new filter object and add to new film
            this.addSelectedFilter(selection, newFilm);
            // add new film object to films list
            data.push(newFilm);
          }
        });
      });
      return data;
    }
  },
  methods: {
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