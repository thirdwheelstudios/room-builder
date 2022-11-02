<script setup lang="ts">
import { computed } from 'vue'
import * as konva from 'konva'

const shapeConfig = computed(() => {
  return {
    sceneFunc: (context: konva.default.Context, shape: konva.default.Shape) => {
      context.beginPath()
      context.moveTo(100, 100)
      context.lineTo(100, 90)
      context.lineTo(70, 90)
      context.quadraticCurveTo(70, 60, 100, 60)

      context.fillStrokeShape(shape)
    },
    stroke: 'black',
    strokeWidth: 4,
  }
})
</script>

<template>
  <v-shape :config="shapeConfig" draggable="true" />
</template>
