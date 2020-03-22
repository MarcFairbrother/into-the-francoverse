<template>
  <div>
    <h2>Films</h2>
    <button @click="addNewSelection">Add New Selection</button>
    <Filters
      v-for="(selection, i) in reactiveSelections"
      :key="i"
      :film-selection="selection"
      :selection-id="i"
      @removeSelection="deleteFromArray(filmSelections, $event)"
      @selectFilter="filterSelection"
      @removeFilter="
        filterRemove($event.target.dataset.selectionid, $event.target.value)
      "
    />
    <Chart />
    <List />
  </div>
</template>

<script>
import Filters from "./Filters";
import Chart from "./Chart";
import List from "./List";

export default {
  name: "Films",
  components: {
    Filters,
    Chart,
    List
  },
  data: function() {
    return {
      films: [
        {
          title: "L'horrible Docteur Orlof",
          year: 1962,
          cast: ["Diana Loris", "Howard Vernon"],
          genres: ["pulp", "horror"]
        },
        {
          title: "Le sadique Baron Von Klaus",
          year: 1962,
          cast: ["Howard Vernon", "Paula Martel"],
          genres: ["pulp", "horror"]
        },
        {
          title: "Certains l'aiment noire",
          year: 1962,
          cast: ["Antonio Ozores", "Lina Morgan"],
          genres: ["pulp", "detective"]
        },
        {
          title: "Le Jaguar",
          year: 1963,
          cast: ["Sylvia Sorrente", "Todd Martin"],
          genres: ["pulp"]
        },
        {
          title: "Chasse à la mafia",
          year: 1963,
          cast: ["Jean Servais", "Laura Granados"],
          genres: ["pulp", "detective"]
        },
        {
          title: "Cartes sur table",
          year: 1966,
          cast: ["Eddie Constantine", "Françoise Brion", "Fernando Rey"],
          genres: ["pulp", "detective"]
        },
        {
          title: "Dans les griffes du maniaque",
          year: 1966,
          cast: ["Estella Blain", "Mabel Karr", "Howard Vernon"],
          genres: ["pulp", "horror"]
        },
        {
          title: "Opération Re Mida",
          year: 1967,
          cast: ["Ray Danton", "Barbara Bold", "Dante Posani"],
          genres: ["pulp"]
        },
        {
          title: "Les Yeux verts du diable",
          year: 1968,
          cast: ["Janine Reynaud", "Jack Taylor", "Adrian Hoven"],
          genres: ["pulp"]
        },
        {
          title: "Le Sang de Fu Manchu",
          year: 1968,
          cast: ["Christopher Lee", "Richard Greene", "Maria Rohm"],
          genres: ["pulp"]
        },
        {
          title: "Les Infortunes de la vertu",
          year: 1969,
          cast: ["Klaus Kinski", "Romina Power", "Maria Rohm"],
          genres: ["erotica"]
        },
        {
          title: "Les Inassouvies",
          year: 1970,
          cast: ["Maria Rohm", "Marie Liljedahl", "Christopher Lee"],
          genres: ["erotica", "psychedelic"]
        },
        {
          title: "Le Trône de feu",
          year: 1970,
          cast: ["Christopher Lee", "Maria Schell", "Howard Vernon"],
          genres: ["horror", "period"]
        }
      ],
      filmSelections: []
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
        const newSelection = {
          currentFilms: filteredFilms,
          selectedFilters: selection.selectedFilters,
          cast: this.getValuesCount(filteredFilms, selectedCast, "cast"),
          selectedCast: selectedCast,
          genres: this.getValuesCount(filteredFilms, selectedGenres, "genres"),
          selectedGenres: selectedGenres
        };
        data.push(newSelection);
      });
      return data;
    }
  },
  methods: {
    // adds a new object to the existing film selections array
    addNewSelection: function() {
      this.filmSelections.push({
        currentFilms: this.films,
        selectedFilters: []
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
        selectedFilters: []
      }
    ];
  }
};
</script>