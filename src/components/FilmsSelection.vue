<template>
  <li class="selection" :style="`background-color: ${selectionColor}`">
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
  computed: {
    selectionColor: function() {
      return Object.values(this.filmSelection.color)[0];
    }
  },
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

<style lang="scss" scoped>
.selection {
  border-radius: 50px;
  color: var(--off-white);
  & > article {
    background: url("data:image/svg+xml; utf8, %3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%2248%22%20height%3D%2248%22%20viewBox%3D%220%200%2012.7%2012.7%22%3E%3Cg%20fill%3D%22%23f1f0e9%22%20paint-order%3D%22fill%20markers%20stroke%22%3E%3Cpath%20d%3D%22M0%208.467h12.7v2.117H0zM0%204.233h12.7V6.35H0zM0%200h12.7v2.117H0z%22%2F%3E%3C%2Fg%3E%3C%2Fsvg%3E");
    background-position: bottom;
    background-repeat: repeat-x;
    background-size: 3rem;
    display: flex;
    flex-direction: column;
    padding: 4rem;
    & > h3 {
      font-size: 3rem;
      margin-bottom: 2rem;
    }
    & > p,
    & > button {
      font-size: 2rem;
      font-weight: 400;
      margin-bottom: 2rem;
    }
  }
}
</style>