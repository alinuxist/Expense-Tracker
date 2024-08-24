<script setup>
import Header from "@/components/Header.vue";
import Balance from "@/components/Balance.vue";
import IncomeExpenses from "@/components/IncomeExpenses.vue";
import TransactionList from "@/components/TransactionList.vue";
import AddTransaction from "@/components/AddTransaction.vue";
import {computed, onMounted, ref} from "vue";
import {useToast} from "vue-toastification";




const transactions = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));

  if (savedTransactions){
    transactions.value = savedTransactions;
  }

});

const toast = useToast();

const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0).toFixed(2);
})

const income = computed(() => {
  return transactions.value
      .filter((transaction) => transaction.amount > 0)
      .reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0).toFixed(2);
})


const expense = computed(() => {
  return transactions.value
      .filter((transaction) => transaction.amount < 0)
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0).toFixed(2);
})



const handleTransactionSubmit = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });

  saveTransactionsToLocalStorage();

  toast.success("Transaction Added Successfully!");
};

const handleDeleteTransaction = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id);

  saveTransactionsToLocalStorage();

  toast.error("Transaction Deleted Successfully!");
};

const generateUniqueId = () => {
  return Math.floor(Math.random() * 100000);
};


const saveTransactionsToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};


</script>

















<template>
  <Header/>

  <div class="container my-2.5">
    <Balance :total="+total"/>
  </div>

  <income-expenses :income="+income" :expense="+expense"/>

  <div class="flex max-w-96 flex-col my-5">
    <transaction-list @transactionDeleted="handleDeleteTransaction" :transactions="transactions"/>
  </div>

  <AddTransaction @addTransaction="handleTransactionSubmit"/>

</template>
