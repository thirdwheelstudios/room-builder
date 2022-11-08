<script setup lang="ts">
import { computed } from 'vue'

interface Props {
  externalDoor?: boolean
  draggable?: boolean
  selected?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  externalDoor: true,
  draggable: true,
  selected: false,
})

const strokeColor = computed(() => {
  return props.selected ? 'red' : 'white'
})

const doorLineConfig = computed(() => {
  return {
    stroke: strokeColor.value,
    strokeWidth: 2,
    closed: false,
    lineCap: 'round',
    points: [100, 95, 100, 90, 70, 90],
  }
})

const doorArcConfig = computed(() => {
  return {
    stroke: strokeColor.value,
    strokeWidth: 2,
    closed: false,
    lineCap: 'round',
    points: [70, 90, 80, 70, 100, 60],
    tension: 0.5,
  }
})

const externalDoorConfig = computed(() => {
  return {
    stroke: strokeColor.value,
    strokeWidth: 2,
    closed: false,
    points: [100, 60, 100, 90],
    dash: [2],
  }
})
</script>

<template>
  <v-group :draggable="draggable">
    <v-line :config="doorLineConfig" />
    <v-line :config="doorArcConfig" />
    <v-line v-if="externalDoor" :config="externalDoorConfig" />
  </v-group>
</template>
