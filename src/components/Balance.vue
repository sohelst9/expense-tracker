<template>
    <div class="balance-section">
        <div class="balance-label">YOUR BALANCE</div>
        <div class="balance">${{ balance }}</div>
    </div>
</template>

<script setup>

const props = defineProps({
    balance: {
        type: Number,
        required: true
    }
});
</script>