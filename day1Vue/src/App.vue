<template>
  <HeaderComponent/>
  <div class="container">
    <BalanceComponent :total = "total"/>
    <IncomeExpense :income ="income" :expense = "expense"/>
    <TransactionList :transactions="transactions"/>
    <AddTransaction/>
  </div>
</template>

<script setup>
import AddTransaction from './components/AddTransaction.vue';
import BalanceComponent from './components/BalanceComponent.vue';
import HeaderComponent from './components/HeaderComponent.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';
import {ref, computed} from 'vue'
const transactions = ref([
    {
        id: 1, text: "Sword", amount: -20000
    },
    {
        id: 2, text: "Shield", amount: 200000
    },
    {
        id: 3, text: "Armor", amount: 600000
    }
]);
const total = computed(() => {
  return transactions.value.reduce((acc,transaction)=> {
    return acc + transaction.amount;
    }, 0)
})

const income = computed(() => {
  return transactions.value
  .filter((transaction)=> transaction.amount > 0)
  .reduce((acc,transaction)=> {
    return acc + transaction.amount;
    }, 0).toFixed(2)
})

const expense = computed(() => {
  return transactions.value
  .filter((transaction)=> transaction.amount < 0)
  .reduce((acc,transaction)=> {
    return acc + transaction.amount;
    }, 0).toFixed(2)
})
</script>