<template>
  <div>
    <h3>Selection {{ selectionId + 1 }}</h3>
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
      name="composers"
      id="composers-select"
      @change="
        selectFilter(selectionId, 'composers', 'selectedComposers', $event)
      "
    >
      <option value="">Composers</option>
      <option v-for="(value, i) in filmSelection.composers" :key="i" :value="i">
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
      name="producers"
      id="producers-select"
      @change="
        selectFilter(selectionId, 'producers', 'selectedProducers', $event)
      "
    >
      <option value="">Producers</option>
      <option v-for="(value, i) in filmSelection.producers" :key="i" :value="i">
        {{ i }} ({{ value }})
      </option>
    </select>
    <select
      name="pseudonyms"
      id="pseudonyms-select"
      @change="
        selectFilter(selectionId, 'pseudonyms', 'selectedPseudonyms', $event)
      "
    >
      <option value="">Pseudonyms</option>
      <option
        v-for="(value, i) in filmSelection.pseudonyms"
        :key="i"
        :value="i"
      >
        {{ i }} ({{ value }})
      </option>
    </select>
    <select
      name="colors"
      id="colors-select"
      :data-selectionId="selectionId"
      @change="selectColor($event)"
    >
      <option v-for="(color, k, i) in colors" :key="i" :value="k">
        {{ k }}
      </option>
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
  props: ["filmSelection", "selectionId", "availableColors"],
  computed: {
    colors: function() {
      return { ...this.filmSelection.colorChoices, ...this.availableColors };
    }
  },
  methods: {
    // fires a custom event when user deletes this selection
    removeSelection(index) {
      this.$emit("removeSelection", index);
    },
    // fires a custom event when a color is selected
    selectColor(e) {
      this.$emit("selectColor", e);
      this.resetSelect(e.target);
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