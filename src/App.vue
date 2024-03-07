<script setup lang="ts">
import AddTransaction from './components/AddTransaction.vue';
import Balance from './components/Balance.vue';
import Header from './components/Header.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';

</script>

<template>
  <Header/>

  <div class="container">
    <Balance/>
    <IncomeExpense/>
    <TransactionList/>
    <AddTransaction/>
  </div>
 
</template>


