<template>
    <div class="history">
        <h4>Transaction History</h4>
        <div class="history-item" v-for="Transaction in Transactions">
            <div>{{ Transaction.text }}</div>
            <div class="amount negative">$ {{ Transaction.amount }}</div>
        </div>
        
    </div>
</template>

<script setup>
import {defineProps} from 'vue'

const props = defineProps({
    Transactions:{
        type: Array,
        required: true
    }
});
</script>
