<script setup lang="ts">

defineProps(['title'])

</script>

<template>
  <h4>{{ title }}</h4>
  <button @click="$emit('enlarge-text')">Enlarge text</button>
</template>

<style scoped></style>
