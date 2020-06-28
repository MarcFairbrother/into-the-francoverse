<template>
  <div
    class="filters"
    :style="
      `--selection-color: ${selectionColor}; --selection-arrow: url('data:image/svg+xml;utf8,${svgArrow}');`
    "
  >
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
          {{ Object.keys(label)[0] }}: {{ Object.values(label)[0] }}
        </button>
      </li>
    </ul>
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
    },
    selectionColor: function() {
      return Object.values(this.filmSelection.color)[0];
    },
    svgArrow: function() {
      const colorCode = this.selectionColor.substr(1);
      const svg = `%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%2240%22%20height%3D%2230%22%20viewBox%3D%220%200%2010.583333%207.9375005%22%3E%0A%20%20%3Cpath%20d%3D%22M2.4422283%200L0%202.50635l2.8494385%202.92426-.0005292.00054%202.4427575%202.50581%202.442745-2.50582-.0005167-.00053%202.8494389-2.92426L8.1411053%200%205.2916668%202.92425zm2.8494385%207.93696l-.0005292.00054h.0010584z%22%20fill%3D%22%23${colorCode}%22%20paint-order%3D%22fill%20markers%20stroke%22%2F%3E%0A%3C%2Fsvg%3E`;
      return svg;
    }
  },
  methods: {
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
  &__selected {
    display: flex;
    flex-wrap: wrap;
  }
  & select {
    background: var(--off-white) var(--selection-arrow);
    background-repeat: no-repeat;
    background-position: right 2rem top 2.5rem;
    background-size: 2rem;
    border: solid 2px var(--selection-color);
    color: var(--dark-grey);
    color: var(--selection-color);
    font-size: 2rem;
    line-height: 6rem;
    padding: 0 2rem;
    width: 100%;
  }
  & button {
    align-items: center;
    background: var(--selection-color);
    border-radius: 0.5rem;
    color: var(--off-white);
    display: flex;
    font-size: 1.5rem;
    margin-bottom: 2rem;
    margin-right: 2rem;
    padding: 1rem 2rem;
    text-transform: capitalize;
    &::before {
      background: url("data:image/svg+xml; utf8, %3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%220%200%2010.583333%2010.583334%22%3E%0A%20%20%3Cpath%20d%3D%22M0%202.44231l2.849359%202.84935L0%208.14102l2.4423078%202.44231%202.849359-2.84936%202.8493591%202.84936%202.4423071-2.44231-2.8493584-2.84936%202.8493584-2.84935L8.1410259-.00001%205.2916668%202.84935%202.4423078-.00001z%22%20fill%3D%22%23f1f0e9%22%20paint-order%3D%22fill%20markers%20stroke%22%2F%3E%0A%3C%2Fsvg%3E");
      content: "";
      background-size: 1.5rem;
      display: block;
      flex-shrink: 0;
      height: 1.5rem;
      margin-right: 2rem;
      width: 1.5rem;
    }
  }
}
</style>