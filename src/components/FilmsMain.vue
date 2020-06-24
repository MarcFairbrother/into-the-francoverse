<template>
  <main class="films">
    <section class="films__chart">
      <div class="labels--y">
        <ChartLabelsY />
      </div>
      <ChartMain
        :film-selection="reactiveSelections"
        :all-films="films"
        class="graph"
      />
    </section>
    <ul class="films__selections">
      <FilmsSelection
        v-for="(selection, i) in reactiveSelections"
        v-show="!selection.isDisabled"
        :key="i"
        :film-selection="selection"
        :selection-id="i"
        @removeSelection="disableSelection(filmSelections, $event)"
        @editFilters="toggleEditing($event)"
      />
      <li class="add__selection" v-show="activeSelections.length < 4">
        <button @click="addNewSelection">New Selection</button>
      </li>
    </ul>
    <SelectionFilters
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
      class="films__filters"
    />
    <FilmsList :film-selections="activeSelections" class="films__list" />
  </main>
</template>

<script>
import Filmography from "../assets/js/data";
import ChartMain from "./ChartMain";
import ChartLabelsY from "./ChartLabelsY";
import FilmsSelection from "./FilmsSelection";
import SelectionFilters from "./SelectionFilters";
import FilmsList from "./FilmsList";

export default {
  name: "FilmsMain",
  components: {
    ChartMain,
    ChartLabelsY,
    FilmsSelection,
    SelectionFilters,
    FilmsList
  },
  data: function() {
    return {
      films: Filmography,
      filmSelections: [],
      baseColors: [
        { purple: "rgb(102,58,136)" },
        { blue: "rgb(15,95,115)" },
        { green: "rgb(35,130,130)" },
        { lavender: "rgb(156,131,198)" },
        { red: "rgb(215,55,85)" }
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
          isEditing: selection.isEditing,
          isDisabled: selection.isDisabled
        };
        data.push(newSelection);
      });
      return data;
    },
    activeSelections: function() {
      const data = this.reactiveSelections.filter(selection => {
        return !selection.isDisabled;
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
        isEditing: false,
        isDisabled: false
      });
      this.toggleEditing(this.filmSelections.length - 1);
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
    // sets the film selection with passed index to disable and removes color
    disableSelection: function(data, index) {
      data[index].isDisabled = true;
      data[index].color = { transparent: "rgba(0,0,0,0)" };
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
        isEditing: true,
        isDisabled: false
      }
    ];
  },
  updated: function() {
    // if none of the selections are being edited set the first selection to being edited
    const editedSection = this.filmSelections.find(
      selection => selection.isEditing
    );
    if (this.activeSelections.length > 0 && editedSection.isDisabled) {
      const target = this.filmSelections.find(
        selection => !selection.isDisabled
      );
      this.toggleEditing(this.filmSelections.indexOf(target));
    } else if (this.activeSelections.length === 0) {
      this.filmSelections.forEach(selection => {
        selection.isEditing = false;
      });
    }
  }
};
</script>

<style lang="scss">
.films {
  display: grid;
  grid-template-columns: 1fr;
  padding: 0 2rem;
  position: relative;
  @include breakpoint($desktop-width) {
    grid-template-columns: repeat(12, 1fr);
  }
  &__chart {
    grid-row: 1;
    margin-left: 3.5rem;
    overflow-x: scroll;
    overflow-y: hidden;
    @include breakpoint($desktop-width) {
      grid-column: 2/12;
      margin-left: 0;
      margin-top: 4rem;
      overflow: hidden;
      position: relative;
      transform: translateX(-2.5rem);
      width: calc(100% + 2.5rem);
    }
    @include breakpoint($large-width) {
      margin-top: 6rem;
      transform: translateX(-4rem);
      width: calc(100% + 4rem);
    }
    & .graph {
      display: block;
      height: 65vh;
      width: auto;
      @include breakpoint($desktop-width) {
        height: auto;
        margin-left: 2.5rem;
        width: calc(100% - 2.5rem);
      }
      @include breakpoint($large-width) {
        height: auto;
        margin-left: 4rem;
        width: calc(100% - 4rem);
      }
    }
    & .labels--y {
      background: var(--off-white);
      left: 2rem;
      position: absolute;
      top: 0rem;
      @include breakpoint($desktop-width) {
        bottom: 0;
        left: 0;
      }
      & > svg {
        height: 65vh;
        @include breakpoint($desktop-width) {
          height: 100%;
        }
      }
    }
  }
  &__selections {
    display: grid;
    grid-gap: 4rem;
    grid-row: 2;
    grid-template-columns: 1fr;
    margin-top: 1rem;
    @include breakpoint($tablet-width) {
      grid-template-columns: repeat(2, 1fr);
    }
    @include breakpoint($desktop-width) {
      grid-template-columns: repeat(4, 1fr);
      grid-column: 2/12;
    }
    & > .add__selection {
      align-items: center;
      border: solid 1px var(--dark-grey);
      border-radius: 50px;
      display: flex;
      justify-content: center;
      padding: 4rem;
      & > button {
        align-items: center;
        display: flex;
        flex-direction: column;
        font-size: 2rem;
        cursor: pointer;
        &::before {
          background: url("data:image/svg+xml; utf8, %3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%2248%22%20height%3D%2248%22%20viewBox%3D%220%200%2012.7%2012.7%22%3E%3Cpath%20d%3D%22M6.35%200A6.35%206.35%200%20000%206.35a6.35%206.35%200%20006.35%206.35%206.35%206.35%200%20006.35-6.35A6.35%206.35%200%20006.35%200zM5.292%202.117h2.116v3.175h3.175v2.116H7.408v3.175H5.292V7.408H2.117V5.292h3.175V2.117z%22%20fill%3D%22%230a0a0a%22%20paint-order%3D%22fill%20markers%20stroke%22%2F%3E%3C%2Fsvg%3E");
          background-size: 6rem;
          content: "";
          display: block;
          height: 6rem;
          margin: 2rem 0;
          width: 6rem;
        }
      }
    }
  }
  &__filters {
    display: grid;
    grid-gap: 4rem;
    grid-row: 3;
    grid-template-columns: 1fr;
    margin: 6rem 0;
    @include breakpoint($tablet-width) {
      grid-template-columns: repeat(2, 1fr);
    }
    @include breakpoint($desktop-width) {
      grid-template-columns: repeat(3, 1fr);
      grid-column: 2/12;
    }
  }
  &__list {
    display: grid;
    grid-gap: 4rem;
    grid-row: 4;
    grid-template-columns: 1fr;
    @include breakpoint($tablet-width) {
      grid-template-columns: repeat(2, 1fr);
    }
    @include breakpoint($desktop-width) {
      grid-template-columns: repeat(3, 1fr);
      grid-column: 2/12;
    }
    @include breakpoint($large-width) {
      grid-template-columns: repeat(4, 1fr);
    }
  }
}
</style>