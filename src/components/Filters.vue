<template>
  <div>
    <h3>Selection {{ selectionId }}</h3>
    <button @click="removeSelection(selectionId)">Remove Selection</button>
    <p>{{ filmSelection }}</p>
  </div>
</template>

<script>
export default {
  name: "Filters",
  props: ["filmSelection", "selectionId"],
  methods: {
    removeSelection(index) {
      this.$emit("removeSelection", index);
    }
  }
};
</script>