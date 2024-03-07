<template>
  <Header/>
  <div class="container">
    <Balance :total="+total"/>
    <IncomeExpense :income="+income" :expenses="+expenses"/>
    <TransactionList :Transactions="Transactions" @transactionDeleted="handleDelete"/>
    <AddTransaction @transactionSubmitted="handleSubmit"/>
  </div>
 
</template>


<script setup>
import { ref, computed } from 'vue';
import AddTransaction from './components/AddTransaction.vue';
import Balance from './components/Balance.vue';
import Header from './components/Header.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';
import {useToast} from 'vue-toastification';

const toast = useToast();


const generateUniqueId =()=>{
  return Math.floor(Math.random() * 10000)
}

const Transactions = ref([
  { id: 1, text: 'Flower', amount: -20 },
  { id: 2, text: 'Salary', amount: 300 },
  { id: 3, text: 'Book', amount: -10 },
  { id: 4, text: 'Camera', amount: 150 }
]
);

const  handleSubmit =(e)=>{
 Transactions.value.push({
  id: generateUniqueId(),
  text: e.text,
  amount: e.amount
 })
  toast.success('Transaction Added successfully')
}

const handleDelete =(id)=>{
  Transactions.value = Transactions.value.filter((trans)=>trans.id !== id)

  toast.success('Transaction Deleted successfully')
}

//get total
const total = computed(()=>{
  return Transactions.value.reduce((a,transaction)=>{
    return a + transaction.amount
  },0)
})

//get income
const income = computed(()=>{
  return Transactions.value
  .filter((transaction)=>transaction.amount > 0)
  .reduce((a,transaction)=>{
    return a + transaction.amount
  },0).toFixed(2)
})

//get income
const expenses = computed(()=>{
  return Transactions.value
  .filter((transaction)=>transaction.amount < 0)
  .reduce((a,transaction)=>{
    return a + transaction.amount
  },0).toFixed(2)
})
</script>


