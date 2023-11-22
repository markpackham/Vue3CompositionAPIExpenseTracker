<template>
  <Header />
  <div class="container">
    <Balance />
    <IncomeExpenses />
    <TransactionList :transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref } from 'vue';

// Make array reactive via ref
const transactions = ref([
  { id: 1, text: 'Flower', amount: -19.99 },
  { id: 2, text: 'Salary', amount: 229.99 },
  { id: 3, text: 'Book', amount: -10.99 },
  { id: 4, text: 'Tip', amount: 19.99 },
]);
</script>