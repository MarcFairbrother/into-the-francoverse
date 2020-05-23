<template>
  <li>
    <article>
      <h3>Selection {{ selectionId + 1 }}</h3>
      <p>{{ filmSelection.currentFilms.length }} films</p>
      <button @click="removeSelection(selectionId)">Delete Section</button>
      <button @click="editFilters(selectionId)">Edit Filters</button>
    </article>
  </li>
</template>

<script>
export default {
  name: "FilmsSelection",
  props: ["filmSelection", "selectionId"],
  methods: {
    // fires a custom event when user deletes this selection
    removeSelection(index) {
      this.$emit("removeSelection", index);
    },
    editFilters(index) {
      this.$emit("editFilters", index);
    }
  }
};
</script>