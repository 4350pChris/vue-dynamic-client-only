<template>
  <h1>{{ movie.title }}</h1>
  Release Date: {{ movie.release_date }}
  <br>
  Director: {{ movie.director }}
  <br>
  Producer: {{ movie.producer }}
</template>

<script lang="ts" setup>
defineProps({
  movie: {
    type: Object,
    required: true,
  },
})
</script>
