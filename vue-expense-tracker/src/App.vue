<template>
  <Header />
  <div class="container">
    <!-- Add "+"" to values to turn strings into numbers -->
    <Balance :total="+total" />
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { useToast } from 'vue-toastification';
import { computed, ref, onMounted } from 'vue';

const toast = useToast();

// Dummy data
// const transactions = ref([
//   { id: 1, text: 'Flower', amount: -19.99 },
//   { id: 2, text: 'Salary', amount: 229.99 },
//   { id: 3, text: 'Book', amount: -10.99 },
//   { id: 4, text: 'Tip', amount: 19.99 },
// ]);

// Make array reactive via ref
const transactions = ref([]);

// onMounted like useEffect in React
onMounted(() => {
  // Grab from transactions from local storage
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

// Get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
    // start accumulator at 0
  }, 0)
});

// Get income
const income = computed(() => {
  return transactions.value
    // We only care about positive numbers ergo "income"
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
      // 2 decimal places
    }, 0).toFixed(2)
});

// Get expenses
const expenses = computed(() => {
  return transactions.value
    // We only care about negative numbers hence an expense
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
      // 2 decimal places
    }, 0).toFixed(2)
});

// Add transaction
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: crypto.randomUUID(),
    text: transactionData.text,
    amount: transactionData.amount,
  });
  toast.success('Transaction added');
}

// Delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((transactions) => transactions.id !== id);

  toast.success('Transaction deleted')
}

</script>