<template>
  <ClientComponent v-if="client" />
</template>

<script lang="ts" setup generic="T extends AsyncComponentLoader">
import { h, ref, onMounted, defineAsyncComponent, useSlots, type AsyncComponentLoader } from 'vue';

type Props = {
  load: T
}

const props = defineProps<Props>()

type Slots = {
  fallback?: () => any
  error?: () => any
}

defineSlots<Slots>()
const slots = useSlots()

const ClientComponent = defineAsyncComponent({
  loader: props.load,
  loadingComponent: slots.fallback,
  errorComponent: slots.error ?? (() => h("p", "Error loading component")),
  onError: (e) => {
    console.error("Component loading failed:", e)
    throw e
  },
  suspensible: false,
})

const client = ref(false)
onMounted(() => {
  client.value = true
})
</script>
