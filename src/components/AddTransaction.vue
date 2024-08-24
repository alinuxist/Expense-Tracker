<script setup>


  import {ref} from "vue";
  import {useToast} from "vue-toastification";

  const text = ref("");
  const amount = ref("");
  const toast = useToast();
  const emit = defineEmits(["addTransaction"]);

  const onsubmit = () => {

    if (!text.value || !amount.value) {

      return toast.error("Value & Text required.");

    }

    const transactionData = {
      text: text.value,
      amount: parseFloat(amount.value),
    }

    emit("addTransaction" , transactionData);

    text.value = "";
    amount.value = "";

  }

</script>

<template>
  <h4 class="text-white text-lg my-2 font-medium">Add Transaction</h4>

  <form @submit.prevent="onsubmit()" class="flex flex-col gap-2.5">

    <div class="flex justify-center p-1 items-center">
      <label class="flex w-full text-white flex-col">
        <span class="px-3">Text</span>
        <input v-model="text" placeholder="Enter Your Text..." class="bg-stone-800 p-2 rounded-2xl outline-none px-3">
      </label>
    </div>

    <div class="flex justify-center p-1 items-center">
      <label class="flex w-full text-white flex-col">
        <span class="px-3">Amount</span>
        <input v-model="amount" placeholder="Enter your Amount" type="number" class="bg-stone-800 p-2 [appearance:textfield] [&::-webkit-outer-spin-button]:appearance-none [&::-webkit-inner-spin-button]:appearance-none rounded-2xl outline-none px-3">
      </label>
    </div>

    <button class="flex justify-center items-center bg-green-600 text-white my-2 font-bold p-3 rounded-2xl w-full">Add Transaction</button>


  </form>

</template>
