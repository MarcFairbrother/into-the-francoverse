<template>
  <div>
    <h3>Selection {{ selectionId }}</h3>
    <button @click="removeSelection(selectionId)">Remove Selection</button>
    <hr />
    <select
      name="cast"
      id="cast-select"
      @change="selectFilter(selectionId, 'cast', 'selectedCast', $event)"
    >
      <option value="">Actresses and Actors</option>
      <option v-for="(value, i) in filmSelection.cast" :key="i" :value="i">
        {{ i }} ({{ value }})
      </option>
    </select>
    <select
      name="genres"
      id="genres-select"
      @change="selectFilter(selectionId, 'genres', 'selectedGenres', $event)"
    >
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
    // fires a custom event when user deletes this selection
    removeSelection(index) {
      this.$emit("removeSelection", index);
    },
    // fires a custom event when a filter option is selected
    selectFilter(index, filterName, filterType, e) {
      this.$emit("selectFilter", {
        index: index,
        filterName: filterName,
        filterType: filterType,
        filterValue: e.target.value
      });
      this.resetSelect(e.target);
    },
    // resets a select element to the first option
    resetSelect: function(select) {
      select.selectedIndex = 0;
    }
  }
};
</script>