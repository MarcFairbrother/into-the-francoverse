<template>
  <div class="filters">
    <h3 class="filters__heading">Selection {{ selectionId + 1 }}</h3>
    <select
      name="cast"
      id="cast-select"
      @change="selectFilter(selectionId, 'cast', 'selectedCast', $event)"
    >
      <option value="">Actresses and Actors</option>
      <option v-for="(value, i) in cast" :key="i" :value="i">
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
      <option v-for="(value, i) in composers" :key="i" :value="i">
        {{ i }} ({{ value }})
      </option>
    </select>
    <select
      name="genres"
      id="genres-select"
      @change="selectFilter(selectionId, 'genres', 'selectedGenres', $event)"
    >
      <option value="">Genres</option>
      <option v-for="(value, i) in genres" :key="i" :value="i">
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
      <option v-for="(value, i) in producers" :key="i" :value="i">
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
      <option v-for="(value, i) in pseudonyms" :key="i" :value="i">
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
    <ul
      class="filters__selected"
      v-show="filmSelection.selectedFilters.length > 0"
    >
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
    <button class="filters__delete" @click="removeSelection(selectionId)">
      Remove Selection
    </button>
  </div>
</template>

<script>
export default {
  name: "SelectionFilters",
  props: ["filmSelection", "selectionId", "availableColors"],
  computed: {
    colors: function() {
      return { ...this.filmSelection.colorChoices, ...this.availableColors };
    },
    cast: function() {
      const data = {};
      this.sortObjectAlpha(this.filmSelection.cast, data);
      return data;
    },
    composers: function() {
      const data = {};
      this.sortObjectAlpha(this.filmSelection.composers, data);
      return data;
    },
    genres: function() {
      const data = {};
      this.sortObjectAlpha(this.filmSelection.genres, data);
      return data;
    },
    producers: function() {
      const data = {};
      this.sortObjectAlpha(this.filmSelection.producers, data);
      return data;
    },
    pseudonyms: function() {
      const data = {};
      this.sortObjectAlpha(this.filmSelection.pseudonyms, data);
      return data;
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
    },
    // returns a new object alphabetically ordered by key from the source object
    sortObjectAlpha: function(src, target) {
      Object.keys(src)
        .sort()
        .forEach(function(key) {
          target[key] = src[key];
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.filters {
  &__heading,
  &__selected,
  &__delete {
    @include breakpoint($tablet-width) {
      grid-column: 1/3;
    }
    @include breakpoint($desktop-width) {
      grid-column: 1/4;
    }
  }
}
</style>