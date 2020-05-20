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
            film.colors.push(selection.color);
            // Add selected filters
          } else {
            film.colors = [selection.color];
            data.push(film);
            // Add selected filters
          }
        });
      });
      return data;
    }
  }
};
</script>