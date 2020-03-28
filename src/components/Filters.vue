<template>
  <div>
    <h3 :style="{ color: filmSelection.color }">Selection {{ selectionId }}</h3>
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
    <select
      name="colors"
      id="colors-select"
      :data-selectionId="selectionId"
      @change="selectColor($event)"
    >
      <option value="#000">Black</option>
      <option value="#32a852">Green</option>
      <option value="#2190a3">Blue</option>
    </select>
    <ul>
      <li v-for="(label, i) in filmSelection.selectedFilters" :key="i">
        <button
          :data-item="i"
          :value="i"
          :data-selectionId="selectionId"
          @click="removeFilter($event)"
        >
          {{ label }}
        </button>
      </li>
    </ul>
    <button @click="removeSelection(selectionId)">Remove Selection</button>
    <hr />
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
    // fires a custom event when a color is selected
    selectColor(e) {
      this.$emit("selectColor", e);
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
    // fires a custom event when a filter option is removed
    removeFilter(e) {
      this.$emit("removeFilter", e);
    },
    // resets a select element to the first option
    resetSelect: function(select) {
      select.selectedIndex = 0;
    }
  }
};
</script>