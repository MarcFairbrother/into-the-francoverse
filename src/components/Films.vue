<template>
  <main>
    <h3>
      <span>Maniacs &amp; Vampires! Sex, Lust &amp; Murder!</span>
      <br />Charting the wonderfully weird worlds of Jess Franco!
    </h3>
    <section class="graph">
      <div class="chart__labels--y">
        <ChartLabelsY />
      </div>
      <Chart :film-selection="reactiveSelections" :all-films="films" />
    </section>
    <ul class="film__selections">
      <FilmSelection
        v-for="(selection, i) in reactiveSelections"
        :key="i"
        :film-selection="selection"
        :selection-id="i"
        @removeSelection="deleteFromArray(filmSelections, $event)"
        @editFilters="toggleEditing($event)"
      />
      <li v-show="reactiveSelections.length < 4">
        <button @click="addNewSelection">Add New Selection</button>
      </li>
    </ul>
    <Filters
      v-for="(selection, i) in reactiveSelections"
      v-show="selection.isEditing"
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
    <FilmsList :film-selections="reactiveSelections" />
  </main>
</template>

<script>
import Filters from "./Filters";
import Chart from "./Chart";
import ChartLabelsY from "./ChartLabelsY";
import FilmsList from "./FilmsList";
import FilmSelection from "./FilmSelection";
import Filmography from "../assets/js/data";

export default {
  name: "Films",
  components: {
    Filters,
    Chart,
    ChartLabelsY,
    FilmSelection,
    FilmsList
  },
  data: function() {
    return {
      films: Filmography,
      filmSelections: [],
      baseColors: [
        { brown: "rgb(125,75,35)" },
        { blue: "rgb(25,75,95)" },
        { green: "rgb(95,125,100)" },
        { purple: "rgb(95,50,90)" },
        { red: "rgb(150,30,20)" }
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
        const selectedComposers = this.referenceArray(
          selection.selectedFilters,
          "composers"
        );
        const selectedGenres = this.referenceArray(
          selection.selectedFilters,
          "genres"
        );
        const selectedProducers = this.referenceArray(
          selection.selectedFilters,
          "producers"
        );
        const selectedPseudonyms = this.referenceArray(
          selection.selectedFilters,
          "pseudonyms"
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
          composers: this.getValuesCount(
            filteredFilms,
            selectedComposers,
            "composers"
          ),
          selectedComposers: selectedComposers,
          genres: this.getValuesCount(filteredFilms, selectedGenres, "genres"),
          selectedGenres: selectedGenres,
          producers: this.getValuesCount(
            filteredFilms,
            selectedProducers,
            "producers"
          ),
          selectedProducers: selectedProducers,
          pseudonyms: this.getValuesCount(
            filteredFilms,
            selectedPseudonyms,
            "pseudonyms"
          ),
          selectedPseudonyms: selectedPseudonyms,
          color: selection.color,
          colorChoices: { ...colorChoices },
          isEditing: selection.isEditing
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
        },
        isEditing: false
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
    // disable editing for all selections and enable for target selection
    toggleEditing: function(e) {
      this.filmSelections.forEach(selection => {
        selection.isEditing = false;
      });
      this.filmSelections[e].isEditing = true;
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
        },
        isEditing: true
      }
    ];
  },
  updated: function() {
    // if none of the selections are being edited set the first selection to being edited
    if (
      this.filmSelections.length > 0 &&
      !this.filmSelections.some(selection => selection.isEditing === true)
    ) {
      this.filmSelections[0].isEditing = true;
    }
  }
};
</script>

<style lang="scss">
main {
  background: rgb(232, 224, 184);
  display: grid;
  grid-template-columns: 1fr 400px 1fr;
  padding: 15px;
  @include breakpoint($tablet-width) {
    grid-template-columns: 1fr 680px 1fr;
  }
  @include breakpoint($desktop-width) {
    grid-template-columns: 1fr 920px 1fr;
  }
  @include breakpoint($large-width) {
    grid-template-columns: 1fr 1020px 1fr;
  }
  & > h3 {
    grid-column: 2;
    grid-row: 1;
    color: var(--pulp-red);
    font-family: "Changa One", Arial, Helvetica, sans-serif;
    font-size: 12px;
    letter-spacing: 1px;
    line-height: 1.5;
    @include breakpoint($tablet-width) {
      font-size: 20px;
      line-height: 1.25;
    }
    & > span {
      color: var(--dark-grey);
      font-size: 18px;
      @include breakpoint($tablet-width) {
        font-size: 28px;
      }
    }
  }
  & .film__selections {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-column: 2;
    grid-row: 3;
    list-style-type: none;
  }
}
.graph {
  grid-column: 2;
  grid-row: 2;
  position: relative;
  width: 100%;
  & > .chart {
    width: 100%;
    display: block;
  }
  & > .chart__labels--y {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 100%;
    width: 17px;
    & > svg {
      height: 100%;
    }
  }
}
div {
  grid-column: 2;
}
</style>