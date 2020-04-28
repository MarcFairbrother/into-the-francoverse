<template>
  <div>
    <h2>Films</h2>
    <button @click="addNewSelection">Add New Selection</button>
    <Filters
      v-for="(selection, i) in reactiveSelections"
      :key="i"
      :film-selection="selection"
      :selection-id="i"
      :available-colors="availableColors"
      @removeSelection="deleteFromArray(filmSelections, $event)"
      @selectColor="colorSelection"
      @selectFilter="filterSelection"
      @removeFilter="
        filterRemove($event.target.dataset.selectionid, $event.target.value)
      "
    />
    <section class="graph">
      <Chart :film-selection="reactiveSelections" :all-films="films" />
    </section>
    <List />
  </div>
</template>

<script>
import Filters from "./Filters";
import Chart from "./Chart";
import List from "./List";
import Filmography from "../assets/data";

export default {
  name: "Films",
  components: {
    Filters,
    Chart,
    List
  },
  data: function() {
    return {
      films: Filmography,
      filmSelections: [],
      baseColors: [
        { yellow: "#fcba03" },
        { blue: "#36a891" },
        { green: "#169128" },
        { pink: "#ad18a8" },
        { red: "#ab0f31" }
      ]
    };
  },
  computed: {
    reactiveSelections: function() {
      const data = [];
      this.filmSelections.forEach(selection => {
        const filteredFilms = this.getFilteredFilms(
          selection.selectedFilters,
          selection.currentFilms
        );
        const selectedCast = this.referenceArray(
          selection.selectedFilters,
          "cast"
        );
        const selectedGenres = this.referenceArray(
          selection.selectedFilters,
          "genres"
        );
        const colorChoices = {};
        for (let i in selection.color) {
          colorChoices[i] = selection.color[i];
        }
        const newSelection = {
          currentFilms: filteredFilms,
          selectedFilters: selection.selectedFilters,
          cast: this.getValuesCount(filteredFilms, selectedCast, "cast"),
          selectedCast: selectedCast,
          genres: this.getValuesCount(filteredFilms, selectedGenres, "genres"),
          selectedGenres: selectedGenres,
          color: selection.color,
          colorChoices: { ...colorChoices }
        };
        data.push(newSelection);
      });
      return data;
    },
    shuffledColors: function() {
      return this.shuffleArray(this.baseColors);
    },
    selectedColors: function() {
      const data = [];
      this.reactiveSelections.forEach(selection => {
        data.push(Object.keys(selection.color)[0]);
      });
      return data;
    },
    availableColors: function() {
      const data = {};
      this.shuffledColors.forEach(color => {
        for (let i in color) {
          if (!this.selectedColors.includes(i)) {
            data[i] = color[i];
          }
        }
      });
      return data;
    }
  },
  methods: {
    // adds a new object to the existing film selections array
    addNewSelection: function() {
      this.filmSelections.push({
        currentFilms: this.films,
        selectedFilters: [],
        color: {
          [Object.keys(this.availableColors)[0]]: this.availableColors[
            Object.keys(this.availableColors)[0]
          ]
        }
      });
    },
    // creates an object listing all values and number of occurences in an array field of a film object
    getValuesCount: function(data, reference, field) {
      const values = [];
      const valuesCount = {};
      // creates an array containing all the values
      data.forEach(item => {
        values.push(...item[field]);
      });
      // udpates an object containing the values with the total count
      values.forEach(item => {
        if (reference.includes(item)) {
          return;
        } else if (valuesCount[item]) {
          valuesCount[item]++;
        } else {
          valuesCount[item] = 1;
        }
      });
      return valuesCount;
    },
    // removes item with passed index from passed array
    deleteFromArray: function(data, index) {
      data.splice(index, 1);
    },
    // updates color on selectColor custom event
    colorSelection: function(e) {
      this.filmSelections[e.target.dataset.selectionid].color = {
        [e.target.value]: this.availableColors[e.target.value]
      };
    },
    // updates selected filters on selectFilter custom event
    filterSelection: function(e) {
      const data = this.filmSelections[e.index];
      data.selectedFilters.push({
        [e.filterName]: e.filterValue
      });
    },
    // handles removing option from active filters
    filterRemove: function(index, data) {
      this.deleteFromArray(this.filmSelections[index].selectedFilters, data);
    },
    // returns an array of films matching an array of filters
    getFilteredFilms: function(selectedFilters, data) {
      if (selectedFilters.length === 0) {
        return data;
      } else {
        let updatedFilms = data;
        selectedFilters.forEach(item => {
          for (let i in item) {
            updatedFilms = this.filterBy(updatedFilms, i, item[i]);
          }
        });
        return updatedFilms;
      }
    },
    // filters an array of objects searching the field property for a value matching name
    filterBy: function(data, field, name) {
      return data.filter(item => item[field].includes(name));
    },
    // builds a refence array containing all values from an array of objects
    referenceArray: function(data, type) {
      const result = [];
      data.forEach(item => {
        for (const i in item) {
          if (i === type) {
            result.push(item[i]);
          }
        }
      });
      return result;
    },
    // reorders array randomly
    shuffleArray: function(array) {
      const shuffled = array
        .map(a => [Math.random(), a])
        .sort((a, b) => a[0] - b[0])
        .map(a => a[1]);
      return shuffled;
    },
    // use this to log custom events during development
    logEvent: function(value) {
      // eslint-disable-next-line
      console.log(value);
    }
  },
  mounted: function() {
    // creates first unfiltered film selection when component is mounted
    this.filmSelections = [
      {
        currentFilms: this.films,
        selectedFilters: [],
        color: {
          [Object.keys(this.availableColors)[0]]: this.availableColors[
            Object.keys(this.availableColors)[0]
          ]
        }
      }
    ];
  }
};
</script>

<style>
.graph {
  width: 100%;
}
.graph svg {
  width: 100%;
}
</style>