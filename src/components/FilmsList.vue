<template>
  <ul class="films__list">
    <li v-for="(film, i) in selectedFilms" :key="i">
      <h4>{{ film.title }} ({{ film.year }})</h4>
      <p v-for="(color, n) in film.colors" :key="n">{{ color }}</p>
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
            matchingTitle.colors.push(selection.color);
            // Add selected filters
          } else {
            const newFilm = {
              title: film.title,
              year: film.year,
              colors: [selection.color],
              filters: []
            };
            // Add selected filters
            data.push(newFilm);
          }
        });
      });
      return data;
    }
  }
};
</script>