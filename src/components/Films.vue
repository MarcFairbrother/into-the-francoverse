<template>
  <div>
    <p>All Films</p>
    <Filters />
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
  }
};
</script>