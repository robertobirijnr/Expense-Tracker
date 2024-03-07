<template>
  <Header/>
  <div class="container">
    <Balance :total="total"/>
    <IncomeExpense/>
    <TransactionList :Transactions="Transactions"/>
    <AddTransaction/>
  </div>
 
</template>


<script setup>
import { ref, computed } from 'vue';
import AddTransaction from './components/AddTransaction.vue';
import Balance from './components/Balance.vue';
import Header from './components/Header.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';


const Transactions = ref([
  { id: 1, text: 'Flower', amount: -20 },
  { id: 2, text: 'Salary', amount: 300 },
  { id: 3, text: 'Book', amount: -10 },
  { id: 4, text: 'Camera', amount: 150 }
]
);

const total = computed(()=>{
  return Transactions.value.reduce((a,transaction)=>{
    return a + transaction.amount
  },0)
})
</script>


