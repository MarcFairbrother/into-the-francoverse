<template>
  <svg
    version="1.1"
    baseProfile="full"
    xmlns="http://www.w3.org/2000/svg"
    viewBox="-5 0 570 240"
  >
    <g>
      <path
        v-for="(year, i, n) in allYears"
        :key="i"
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        :d="`M${n * 10},205 L${n * 10}, 65`"
      />
      <path
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        d="M-5,200 L565, 200"
      />
      <path
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        d="M-5,190 L565, 190"
      />
      <path
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        d="M-5,180 L565, 180"
      />
      <path
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        d="M-5,170 L565, 170"
      />
      <path
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        d="M-5,160 L565, 160"
      />
      <path
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        d="M-5,150 L565, 150"
      />
      <path
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        d="M-5,140 L565, 140"
      />
      <path
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        d="M-5,130 L565, 130"
      />
      <path
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        d="M-5,120 L565, 120"
      />
      <path
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        d="M-5,110 L565, 110"
      />
      <path
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        d="M-5,100 L565, 100"
      />
      <path
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        d="M-5,90 L565, 90"
      />
      <path
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        d="M-5,80 L565, 80"
      />
      <path
        style="stroke: rgb(195, 190, 150); stroke-width:1;"
        d="M-5,70 L565, 70"
      />
    </g>
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

export default {
  name: "Chart",
  components: { FilmsPath },
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
          coordinates.push(`M${x},${200 - data[property].length * 10}`);
        } else {
          coordinates.push(`L${x},${200 - data[property].length * 10}`);
        }
        x = x + 10;
      }
      return coordinates;
    }
  }
};
</script>