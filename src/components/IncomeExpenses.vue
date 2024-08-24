<script setup>
  const props = defineProps({
    income:{
      type: Number,
      required: true
    },
    expense:{
      type: Number,
      required: true
    }
  })
</script>

<template>

  <div class="flex justify-center items-center p-5 gap-2.5 bg-stone-800 rounded-2xl">
    <div class="flex flex-col justify-center items-center bg-stone-900 rounded-2xl p-3 px-10">
      <h4 class="text-white">Income</h4>
      <h4 class="text-green-500 font-mono">${{ income }}</h4>
    </div>
    <div class="flex flex-col justify-center items-center bg-stone-900 rounded-2xl p-3 px-10">
      <h4 class="text-white">Expense</h4>
      <h4 class="text-red-500 font-mono"> ${{ expense }}</h4>
    </div>
  </div>

</template>
