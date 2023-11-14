<template>
  <HeaderComponent/>
  <div class="container">
    <BalanceComponent/>
    <IncomeExpense/>
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
import {ref} from 'vue'
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
</script>