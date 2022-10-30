<script setup lang="ts">
import { ref } from 'vue'
import * as konva from 'konva'

const configKonva = ref({ width: 300, height: 300 })

const walls = [
  {
    x: 20,
    y: 20,
    width: 6,
    height: 150,
    fill: '#ddd',
    stroke: 'red',
    strokeWidth: 2,
    shadowBlur: 10,
    draggable: true,
  },
  {
    x: 20,
    y: 172,
    width: 260,
    height: 6,
    fill: '#ddd',
    stroke: 'red',
    strokeWidth: 2,
    shadowBlur: 10,
    draggable: true,
  },
  {
    x: 274,
    y: 75,
    width: 6,
    height: 95,
    fill: '#ddd',
    stroke: 'red',
    strokeWidth: 2,
    shadowBlur: 10,
    draggable: true,
  },
  {
    x: 274,
    y: 20,
    width: 6,
    height: 15,
    fill: '#ddd',
    stroke: 'red',
    strokeWidth: 2,
    shadowBlur: 10,
    draggable: true,
  },
  {
    x: 20,
    y: 12,
    width: 260,
    height: 6,
    fill: '#ddd',
    stroke: 'red',
    strokeWidth: 2,
    shadowBlur: 10,
    draggable: true,
  },
]

const doorShapes = [
  {
    fill: '#3399ff',
    stroke: 'blue',
    strokeWidth: 4,
    draggable: true,
    sceneFunc: (context: konva.default.Context, shape: konva.default.Shape) => {
      const x = 274
      const y = 72

      context.beginPath()
      context.moveTo(x, y)
      context.lineTo(x + 6, y)
      context.lineTo(x + 6, y - 8)
      context.lineTo(264, 42)
      context.lineTo(260, 46)
      context.lineTo(x, y - 8)
      context.closePath()

      context.fillStrokeShape(shape)
    },
  },
]

const rectList = ref([...walls])
const shapesList = ref([...doorShapes])
</script>

<template>
  <v-stage :config="configKonva">
    <v-layer
      ><v-rect
        v-for="rect of rectList"
        :x="rect.x"
        :y="rect.y"
        :width="rect.width"
        :height="rect.height"
        :fill="rect.fill"
        :stroke="rect.stroke"
        :stroke-width="rect.strokeWidth"
        :shadow-blur="rect.shadowBlur"
        :draggable="true" />
      <v-shape
        v-for="shape of shapesList"
        :config="{
          sceneFunc: shape.sceneFunc,
          fill: shape.fill,
          stroke: shape.stroke,
          strokeWidth: shape.strokeWidth,
        }"
        :draggable="shape.draggable"
      ></v-shape
    ></v-layer>
  </v-stage>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
