<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li v-for="t in transactions" :key="t.id" :class="t.amount < 0 ? 'minus' : 'plus'">
            {{ t.text }} <span>Rp. {{ t.amount }}</span><button @click="deleteTransaction(transactionId)" class="delete-btn">x</button>
        </li>
        
    </ul>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  transactions: {
    type: Array,
    required: true
  }
})
const emit = defineEmits(['transactionDeleted'])
const deleteTransaction = (Id) => {
  emit('transactionDeleted', id)
}
</script>