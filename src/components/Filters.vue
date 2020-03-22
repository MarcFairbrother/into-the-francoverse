<template>
  <div>
    <h3>Selection {{ selectionId }}</h3>
    <button @click="removeSelection(selectionId)">Remove Selection</button>
    <hr />
    <select name="cast" id="cast-select">
      <option value="">Actresses and Actors</option>
      <option v-for="(value, i) in filmSelection.cast" :key="i" :value="i">
        {{ i }} ({{ value }})
      </option>
    </select>
    <select name="genre" id="genre-select">
      <option value="">Genres</option>
      <option v-for="(value, i) in filmSelection.genres" :key="i" :value="i">
        {{ i }} ({{ value }})
      </option>
    </select>
    <p>Films: {{ filmSelection.currentFilms }}</p>
    <p>Selected Filters: {{ filmSelection.selectedFilters }}</p>
    <p>Cast: {{ filmSelection.cast }}</p>
    <p>Selected Cast: {{ filmSelection.selectedCast }}</p>
    <p>Genres: {{ filmSelection.genres }}</p>
    <p>Selected Genres: {{ filmSelection.selectedGenres }}</p>
  </div>
</template>

<script>
export default {
  name: "Filters",
  props: ["filmSelection", "selectionId"],
  methods: {
    removeSelection(index) {
      this.$emit("removeSelection", index);
    }
  }
};
</script>