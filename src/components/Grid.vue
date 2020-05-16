<template>
  <g>
    <path
      class="count__path"
      data-count="0"
      style="stroke: rgb(195, 190, 150);"
      d="M-5,150 L565, 150"
    />
    <path class="count__path" data-count="1" d="M-5,140 L565, 140" />
    <path class="count__path" data-count="2" d="M-5,130 L565, 130" />
    <path class="count__path" data-count="3" d="M-5,120 L565, 120" />
    <path class="count__path" data-count="4" d="M-5,110 L565, 110" />
    <path class="count__path" data-count="5" d="M-5,100 L565, 100" />
    <path class="count__path" data-count="6" d="M-5,90 L565, 90" />
    <path class="count__path" data-count="7" d="M-5,80 L565, 80" />
    <path class="count__path" data-count="8" d="M-5,70 L565, 70" />
    <path class="count__path" data-count="9" d="M-5,60 L565, 60" />
    <path class="count__path" data-count="10" d="M-5,50 L565, 50" />
    <path class="count__path" data-count="11" d="M-5,40 L565, 40" />
    <path class="count__path" data-count="12" d="M-5,30 L565, 30" />
    <path class="count__path" data-count="13" d="M-5,20 L565, 20" />
    <path
      v-for="(year, i, n) in allYears"
      :key="i"
      :data-year="i"
      class="year__path"
      :d="`M${n * 10},155 L${n * 10}, 15`"
    />
    <text
      v-for="(year, i, n) in allYears"
      :key="n"
      :data-year="i"
      y="172"
      :x="n * 10 - 2"
      fill="rgb(10, 10, 10)"
      class="year__label"
      style="font-family: arial; font-size: 6px;"
      :transform="`rotate(-60, ${n * 10 - 2}, 172)`"
    >
      {{ i }}
    </text>
  </g>
</template>

<script>
export default {
  name: "Grid",
  props: ["allYears", "yearlyCount"],
  mounted: function() {
    const yearLabels = [...document.querySelectorAll(".year__label")];
    yearLabels.forEach(label => {
      this.togglePath(label);
    });
  },
  methods: {
    showPath: function(e) {
      const pathYear = document.querySelector(
        `path[data-year="${e.target.dataset.year}"]`
      );
      pathYear.classList.add("year__path--active");
      this.yearlyCount.forEach(count => {
        const pathYear = document.querySelector(
          `path[data-count="${count[e.target.dataset.year].length}"]`
        );
        pathYear.classList.add("count__path--active");
      });
    },
    hidePath: function(e) {
      const pathYear = document.querySelector(
        `path[data-year="${e.target.dataset.year}"]`
      );
      pathYear.classList.remove("year__path--active");
      this.yearlyCount.forEach(count => {
        const pathYear = document.querySelector(
          `path[data-count="${count[e.target.dataset.year].length}"]`
        );
        pathYear.classList.remove("count__path--active");
      });
    },
    togglePath: function(label) {
      label.addEventListener("mouseover", this.showPath);
      label.addEventListener("mouseout", this.hidePath);
    }
  }
};
</script>

<style lang="scss">
.year__label:hover {
  cursor: pointer;
}
.count__path {
  stroke: rgb(195, 190, 150);
  stroke-width: 1;
  transition: stroke 0.15s ease-out;
  &.count__path--active {
    stroke: rgb(120, 115, 85);
    z-index: 5;
  }
}
.year__path {
  stroke: rgb(195, 190, 150);
  stroke-width: 1;
  transition: stroke 0.15s ease-out;
  z-index: 0;
  &.year__path--active {
    stroke: rgb(120, 115, 85);
  }
}
</style>