<template>
  <div class="add-transaction">
    <h4>Add New Transaction</h4>
    <form @submit.prevent="TrnxSubmit">
      <label for="text">Text</label>
      <input type="text" id="text" v-model="text" placeholder="Enter text...">

      <label for="amount">Amount<br>(negative - expense, positive - income)</label>
      <input type="text" id="amount" v-model="amount" placeholder="Enter amount...">

      <button type="submit">Add Transaction</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useToast } from 'vue-toastification';

const text = ref('');
const amount = ref('');
const Toast = useToast();
const TrnxSubmit = () => {
  if(!text.value || !amount.value){
    Toast.error('Text and Amount Field are required!');
    return;
  }
  console.log(text.value)
  console.log(amount.value)
}
</script>