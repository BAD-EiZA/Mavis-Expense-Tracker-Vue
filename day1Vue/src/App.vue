<template>
  <HeaderComponent />
  <div class="container">
    <BalanceComponent :total="total" />
    <IncomeExpense :income="+income" :expense="+expense" />
    <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>

<script setup>
import AddTransaction from './components/AddTransaction.vue';
import BalanceComponent from './components/BalanceComponent.vue';
import HeaderComponent from './components/HeaderComponent.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';
import { ref, computed, onMounted } from 'vue'
import { useToast } from 'vue-toastification';
const transactions = ref([]);
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0)
})
onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));
  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
})
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2)
})

const expense = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2)
})
const toast = useToast()
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount
  });
  saveTransactionToLocalStorage();
  toast.success("Transaction Added")
}

const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
}

const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );
  saveTransactionToLocalStorage()
  toast.success('Transaction deleted')

}
const saveTransactionToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}
</script>