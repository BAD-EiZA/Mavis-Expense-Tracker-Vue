<template>
  <HeaderComponent/>
  <div class="container">
    <BalanceComponent/>
    <IncomeExpense/>
    <TransactionList/>
  </div>
</template>

<script>
import BalanceComponent from './components/BalanceComponent.vue';
import HeaderComponent from './components/HeaderComponent.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';
export default {
  components: {
    HeaderComponent,
    BalanceComponent,
    IncomeExpense,
    TransactionList
}
}
</script>