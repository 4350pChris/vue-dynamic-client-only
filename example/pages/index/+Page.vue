<template>
  <h1>My Vike app</h1>
  This page is:
  <ul>
    <li>Rendered to HTML.</li>
    <li>Interactive.</li>
  </ul>
  <p>Successful Client Only component</p>
  <ClientOnly :load="load">
    <template #fallback>
      Loading...
    </template>
  </ClientOnly>
  <p>Failed Client Only component</p>
  <ClientOnly :load="fail">
    <template #fallback>
      Loading...
    </template>
    <template #error>
      Error loading component
    </template>
  </ClientOnly>
</template>

<script lang="ts" setup>
import { ClientOnly } from "../../../src"

// const load = () => import("../../components/Counter.vue");
const load = () => new Promise((resolve, reject) => {
  setTimeout(async () => {
    const Counter = await import("../../components/Counter.vue")
    resolve(Counter)
  }, 1000)
})

const fail = () => new Promise((resolve, reject) => {
  setTimeout(() => {
    reject()
  }, 1000)
})
</script>
