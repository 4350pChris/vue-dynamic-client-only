<template>
  <h1>My Vike app</h1>
  This page is:
  <ul>
    <li>Rendered to HTML.</li>
    <li>Interactive.</li>
  </ul>
  <h2>Successful Client Only component</h2>
  <pre>
    <code>
      {{ ` 
<ClientOnly :load="load">
  <template #fallback>
    Loading...
  </template>
</ClientOnly>
      `}}
    </code>
  </pre>
  <ClientOnly :load="load">
    <template #fallback>
      Loading...
    </template>
  </ClientOnly>
  <h2>Failed Client Only component</h2>
  <pre>
    <code>
      {{ `
<ClientOnly :load="fail">
  <template #fallback>
    Loading...
  </template>
  <template #error>
    Error loading component
  </template>
</ClientOnly>
      `}}
    </code>
  </pre>
  <ClientOnly :load="fail">
    <template #fallback>
      Loading...
    </template>
    <template #error>
      Error loading component
    </template>
  </ClientOnly>
  <h2>ClientOnly with sync component</h2>
  <pre>
    <code>
      {{ `
<ClientOnly>
  <p>Default slot</p>
  <template #fallback>
    Loading...
  </template>
</ClientOnly>
      ` }}
    </code>
  </pre>
  <ClientOnly>
    <p>Default slot</p>
    <template #fallback>
      Loading...
    </template>
  </ClientOnly>
</template>

<script lang="ts" setup>
import ClientOnly from "../../../src/components/ClientOnly.vue"

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
