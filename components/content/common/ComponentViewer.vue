<template>
  <ClientOnly>
    <Suspense>
      <template #default>
        <div class="relative">
          <component :key="refreshKey" :is="componentName" />
          <ButtonLink class="absolute -top-12 right-0" left-icon="lucide:refresh-cw" size="xs" variant="outline" @click="refresh"></ButtonLink>
        </div>
      </template>
      <template #fallback>
        <div class="p-4">
          <Spinner class="mx-auto" />
        </div>
      </template>
    </Suspense>
  </ClientOnly>
</template>

<script setup lang="ts">
interface Props {
  componentName?: string;
}

// Define props for the component
defineProps<Props>();


const refreshKey = ref(1)
  function refresh() {
    refreshKey.value +=1
  }
</script>
