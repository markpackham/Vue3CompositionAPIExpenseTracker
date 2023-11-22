<template>
  <Header />
  <div class="container">
    <Balance />
    <IncomeExpenses />
    <TransactionList />
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
</script>