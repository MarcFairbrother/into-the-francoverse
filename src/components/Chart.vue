<template>
  <svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg">
    <g
      v-for="(path, i) in paths"
      :key="i"
      :style="{ stroke: path.color }"
      style="stroke-width: 2;"
    >
      <path
        :d="path.coordinates.join(' ')"
        style="stroke-linejoin: round; fill: none;"
      ></path>
    </g>
  </svg>
</template>

<script>
export default {
  name: "Chart",
  props: ["filmSelection"],
  computed: {
    paths: function() {
      const data = [];
      this.filmSelection.forEach(selection => {
        const filmsByYear = this.listFilmsByYear(
          1960,
          1975,
          selection.currentFilms
        );
        const item = {
          color: selection.color,
          coordinates: this.getCoordinates(filmsByYear)
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
      let x = 10;
      for (const property in data) {
        if (x === 10) {
          coordinates.push(`M${x},${100 - data[property].length * 10}`);
        } else {
          coordinates.push(`L${x},${100 - data[property].length * 10}`);
        }
        x = x + 10;
      }
      return coordinates;
    }
  }
};
</script>