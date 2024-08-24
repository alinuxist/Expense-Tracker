<script setup>
  const props = defineProps({
    total: {
      type: Number,
      required: true,
    }
  })
</script>

<template>
  <h4 class="text-white text-lg font-medium">Your Balance:</h4>
  <h2 class="text-white my-2 text-5xl font-mono">${{ total }}</h2>
</template>
