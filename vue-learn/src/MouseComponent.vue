<script setup lang="ts">
import { useMouse } from './nestedEventExample.ts'

const { x, y } = useMouse()
</script>



<template>Mouse position is at: {{ x }}, {{ y }}</template>

<style scoped></style>
