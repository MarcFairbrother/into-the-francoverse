<template>
  <g :style="{ stroke: pathColor }" style="stroke-width: 2;">
    <path :d="coords" style="stroke-linejoin: round; fill: none;">
      <animate
        attributeName="d"
        :class="pathClass"
        :from="coords"
        :to="this.pathNew"
        dur="1s"
        begin="indefinite"
        fill="freeze"
      />
    </path>
  </g>
</template>

<script>
export default {
  name: "FilmsPath",
  props: ["pathColor", "pathClass", "pathCurrent", "pathNew"],
  data: function() {
    return {
      coords: this.pathCurrent
    };
  },
  watch: {
    pathNew: function() {
      document.querySelector("." + this.pathClass).beginElement();
    }
  },
  mounted: function() {
    document
      .querySelector("." + this.pathClass)
      .addEventListener("endEvent", () => {
        this.coords = this.pathNew;
      });
  }
};
</script>