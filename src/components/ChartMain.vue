<template>
  <svg
    version="1.1"
    baseProfile="full"
    xmlns="http://www.w3.org/2000/svg"
    viewBox="-5 0 570 180"
  >
    <ChartGrid :all-years="allYears" :yearly-count="yearlyCount" />
    <FilmsPath
      v-for="(path, i) in paths"
      :key="i"
      :path-class="'animate' + i"
      :path-color="path.color"
      :path-current="path.currentCoordinates.join(' ')"
      :path-new="path.newCoordinates.join(' ')"
    />
  </svg>
</template>

<script>
import FilmsPath from "./FilmsPath";
import ChartGrid from "./ChartGrid";

export default {
  name: "ChartMain",
  components: { FilmsPath, ChartGrid },
  props: ["filmSelection", "allFilms"],
  data: function() {
    return {
      allYears: this.listAllYears(1958, 2014)
    };
  },
  computed: {
    paths: function() {
      const data = [];
      this.filmSelection.forEach(selection => {
        const item = {
          color: selection.color,
          currentCoordinates: this.getCoordinates(
            this.listFilmsByYear(1958, 2014, this.allFilms)
          ),
          newCoordinates: this.getCoordinates(
            this.listFilmsByYear(1958, 2014, selection.currentFilms)
          )
        };
        data.push(item);
      });
      return data;
    },
    yearlyCount: function() {
      const data = [];
      this.filmSelection.forEach(selection => {
        data.push(this.listFilmsByYear(1958, 2014, selection.currentFilms));
      });
      return data;
    }
  },
  methods: {
    // creates an object listing all years from the first to last years passed as arguments
    listAllYears: function(startYear, endYear) {
      const years = {};
      let currentYear = startYear;
      while (currentYear <= endYear) {
        years[currentYear] = [];
        currentYear++;
      }
      return years;
    },
    // adds an array of films corresponding to each year in years object
    listFilmsByYear: function(startYear, endYear, data) {
      const films = this.listAllYears(startYear, endYear);
      data.forEach(item => {
        films[item.year].push(item.title);
      });
      return films;
    },
    // sets an array of coordinates based on an array of films for each year
    getCoordinates: function(data) {
      const coordinates = [];
      let x = 0;
      for (const property in data) {
        if (x === 0) {
          coordinates.push(`M${x},${150 - data[property].length * 10}`);
        } else {
          coordinates.push(`L${x},${150 - data[property].length * 10}`);
        }
        x = x + 10;
      }
      return coordinates;
    }
  }
};
</script>