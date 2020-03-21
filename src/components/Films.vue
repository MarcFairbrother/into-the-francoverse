<template>
  <div>
    <h2>Films</h2>
    <Filters
      v-for="(selection, i) in filmSelections"
      :key="i"
      :film-selection="selection"
      :selection-id="i"
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
          genre: ["pulp", "horror"]
        },
        {
          title: "Le sadique Baron Von Klaus",
          year: 1962,
          cast: ["Howard Vernon", "Paula Martel"],
          genre: ["pulp", "horror"]
        },
        {
          title: "Certains l'aiment noire",
          year: 1962,
          cast: ["Antonio Ozores", "Lina Morgan"],
          genre: ["pulp", "detective"]
        },
        {
          title: "Le Jaguar",
          year: 1963,
          cast: ["Sylvia Sorrente", "Todd Martin"],
          genre: ["pulp"]
        },
        {
          title: "Chasse à la mafia",
          year: 1963,
          cast: ["Jean Servais", "Laura Granados"],
          genre: ["pulp", "detective"]
        },
        {
          title: "Cartes sur table",
          year: 1966,
          cast: ["Eddie Constantine", "Françoise Brion", "Fernando Rey"],
          genre: ["pulp", "detective"]
        },
        {
          title: "Dans les griffes du maniaque",
          year: 1966,
          cast: ["Estella Blain", "Mabel Karr", "Howard Vernon"],
          genre: ["pulp", "horror"]
        },
        {
          title: "Opération Re Mida",
          year: 1967,
          cast: ["Ray Danton", "Barbara Bold", "Dante Posani"],
          genre: ["pulp"]
        },
        {
          title: "Les Yeux verts du diable",
          year: 1968,
          cast: ["Janine Reynaud", "Jack Taylor", "Adrian Hoven"],
          genre: ["pulp"]
        },
        {
          title: "Le Sang de Fu Manchu",
          year: 1968,
          cast: ["Christopher Lee", "Richard Greene", "Maria Rohm"],
          genre: ["pulp"]
        },
        {
          title: "Les Infortunes de la vertu",
          year: 1969,
          cast: ["Klaus Kinski", "Romina Power", "Maria Rohm"],
          genre: ["erotica"]
        },
        {
          title: "Les Inassouvies",
          year: 1970,
          cast: ["Maria Rohm", "Marie Liljedahl", "Christopher Lee"],
          genre: ["erotica", "psychedelic"]
        },
        {
          title: "Le Trône de feu",
          year: 1970,
          cast: ["Christopher Lee", "Maria Schell", "Howard Vernon"],
          genre: ["horror", "period"]
        }
      ],
      filmSelections: []
    };
  },
  mounted: function() {
    this.filmSelections = [
      {
        currentFilms: this.films,
        selectedFilters: [],
        oldCoords: [],
        newCoords: []
      }
    ];
  }
};
</script>