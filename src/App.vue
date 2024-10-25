<template>
  <div class="wrapper">
    <div class="container">
      <Header />
      <Balance :balance="balance" />
      <ExpenseIcomeShow :income="Totalincome" :expense="Totalexpense" />
      <TransactionList :Transactions="Transactions" />
      <TransactionAdd />


    </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import ExpenseIcomeShow from './components/ExpenseIcomeShow.vue';
import TransactionList from './components/TransactionList.vue';
import TransactionAdd from './components/TransactionAdd.vue';
import { ref, computed } from 'vue';

//---transaction list--
const Transactions = ref([
  { id: 1, text: "Bajar", amount: 100.25889 },
  { id: 2, text: "Shoping", amount: 500 },
  { id: 3, text: "Gift", amount: -300 },
  { id: 3, text: "Gift", amount: -200.58544 },
]);

//--- total balance 
const balance = computed(() => {
  return Transactions.value.reduce((accumulate, transcation) => {
    return accumulate + transcation.amount
  }, 0).toFixed(2)
});

//--- total income
const Totalincome = computed(() => {
  return Transactions.value
    .filter((transcation) => transcation.amount > 0)
    .reduce((accumulate, transcation) => {
      return accumulate + transcation.amount;
    }, 0)
    .toFixed(2);
});

//--- total expense 
const Totalexpense = computed(() => {
  return Transactions.value
    .filter((transcation) => transcation.amount < 0)
    .reduce((accumulate, transcation) => {
      return accumulate + transcation.amount;
    }, 0)
    .toFixed(2);
});

</script>