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

//-- variables
const text = ref('');
const amount = ref('');

//--define emit  and toast 
const emit = defineEmits(['TrnxSubmitted']);
const Toast = useToast();

//-- fucntion to submit transaction
const TrnxSubmit = () => {

  //---check if text and amount are not empty
  if (!text.value || !amount.value) {
    Toast.error('Text and Amount Field are required!');
    return;
  }

  // Create a transaction object with the current text and amount values
  const trnxData = {
    text: text.value,
    amount: parseFloat(amount.value)
  };

  //-- emit the transaction data to parent component
  emit('TrnxSubmitted', trnxData);
  text.value = '';
  amount.value = '';

}
</script>