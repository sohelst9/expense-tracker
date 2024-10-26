<template>
    <div class="history">
        <h4>Transaction History</h4>
        <div class="history-item" v-for="Transaction in Transactions" :key="Transaction.id">
            <div>{{ Transaction.text }}</div>
            <div class="amount" :class="Transaction.amount >= 0 ? 'positive' : 'negative' ">$ {{ Transaction.amount }}</div>
            <div class="trnx_delete" @click="deleteTrnx(Transaction.id)">Delete</div>
        </div>

    </div>
</template>

<script setup>
import { defineProps } from 'vue'

const emit = defineEmits(['deletedTrnx']);
const props = defineProps({
    Transactions: {
        type: Array,
        required: true
    }
});

const deleteTrnx = (id) => {
    emit('deletedTrnx', id);
}
</script>
