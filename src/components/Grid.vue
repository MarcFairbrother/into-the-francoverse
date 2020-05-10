<template>
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
    <text
      v-for="(year, i, n) in allYears"
      :key="n"
      y="222"
      :x="n * 10 - 2"
      fill="rgb(10, 10, 10)"
      style="font-family: arial; font-size: 6px;"
      :transform="`rotate(-60, ${n * 10 - 2}, 222)`"
    >
      {{ i }}
    </text>
  </g>
</template>

<script>
export default {
  name: "Grid",
  props: ["allYears"]
};
</script>