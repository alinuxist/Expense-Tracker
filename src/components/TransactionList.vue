<script setup>
  const props = defineProps({
    transactions: {
      type: Array,
      required: true,
    }
  })

  const emit = defineEmits(["transactionDeleted"]);

  const deleteTransaction = (id) => {
    emit("transactionDeleted", id);
  };
</script>

<template>
  <h2 class="text-white">
    History
  </h2>

  <div class="flex w-full h-0.5 my-1 bg-stone-800 rounded-full"></div>

  <ul>

    <li v-for="transaction in transactions" :key="transaction.id">
      <div class="flex justify-end items-center relative group">
        <button @click="deleteTransaction(transaction.id)" class="flex text-white text-lg tracking-tighter absolute left-0 opacity-0 transition-all justify-center w-12 rounded-2xl group-hover:opacity-100 bg-red-800 p-2 items-center">
          Del
        </button>
        <div class="flex w-full justify-between items-center my-1 group-hover:w-10/12 transition-all border-r-8 bg-stone-800 rounded-2xl p-3 px-5" :class="transaction.amount < 0 ? 'border-red-500' : 'border-green-500'">
          <h4 class="text-white line-clamp-1">{{ transaction.text }}</h4>
          <h4 class="text-white">${{ transaction.amount }}</h4>
        </div>
      </div>
    </li>

  </ul>



</template>
