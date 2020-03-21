<template>
  <div>
    <h3>Selection {{ selectionId }}</h3>
    <p>{{ filmSelection }}</p>
  </div>
</template>

<script>
export default {
  name: "Filters",
  props: ["filmSelection", "selectionId"]
};
</script>