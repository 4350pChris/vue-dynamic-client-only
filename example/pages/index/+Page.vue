<template>
  <h1>My Vike app</h1>
  This page is:
  <ul>
    <li>Rendered to HTML.</li>
    <li>Interactive.
      <ClientOnly :load="load">
        <template #fallback>
          Loading...
        </template>
        <template #error>
          Error loading component
        </template>
      </ClientOnly>
    </li>
  </ul>
</template>

<script lang="ts" setup>
import { ClientOnly } from "../../../src"
import Counter from '../../components/Counter.vue';

// const load = () => import("../../components/Counter.vue");
const load = () => new Promise((resolve, reject) => {
  setTimeout(() => {
    // resolve(Counter)
    reject()
  }, 1000)
})
</script>
