<template>
  <div>
    <p>{{ selectedFilms.length }}</p>
    <p>{{ selectedFilms }}</p>
  </div>
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
            // Add colors and selected filters
          } else {
            data.push(film);
          }
        });
      });
      return data;
    }
  }
};
</script>