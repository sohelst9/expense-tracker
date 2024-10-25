<template>
    <div class="income-expense">
        <div class="income">
            <div>INCOME</div>
            <div>${{ income }}</div>
        </div>
        <div class="expense">
            <div>EXPENSE</div>
            <div>${{ expense }}</div>
        </div>
    </div>
</template>

<script setup>
 
 const props = defineProps({
    expense:{
        type:Number,
        required:true
    },
    income:{
        type:Number,
        required:true
    }
 });
 
</script>