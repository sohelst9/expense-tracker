<template>
  <div class="wrapper">
    <div class="container">
      <Header />
      <Balance :balance="+balance" />
      <ExpenseIcomeShow :income="+Totalincome" :expense="+Totalexpense" />
      <TransactionList :Transactions="Transactions" @deletedTrnx="handleDeletedTrnx" />
      <TransactionAdd @TrnxSubmitted="handleTrnxData" />


    </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import ExpenseIcomeShow from './components/ExpenseIcomeShow.vue';
import TransactionList from './components/TransactionList.vue';
import TransactionAdd from './components/TransactionAdd.vue';
import { ref, computed, onMounted } from 'vue';
import { useToast } from 'vue-toastification';

//---transaction list--
const Transactions = ref([]);
const toast = useToast();

//-- check localstorage item
onMounted(() => {
  const SaveTrnxs = JSON.parse(localStorage.getItem('Transactions'));
  if (SaveTrnxs) {
    Transactions.value = SaveTrnxs;
  }
});

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

//--- trnx data push trnx list
const handleTrnxData = (trnxData) => {
  Transactions.value.push({
    id: generateUniqueId(),
    text: trnxData.text,
    amount: trnxData.amount
  });
  saveTrnxData();
  toast.success(' Transaction added successfully! ');
};

//---unique id generate
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
}

//--- handle delete emit 
const handleDeletedTrnx = (id) => {
  Transactions.value = Transactions.value.filter((transcation) => transcation.id !== id);
  toast.success('Transaction Deleted Successfully!');

  saveTrnxData();
}

//--save trnx data to local storage
const saveTrnxData = () => {
  localStorage.setItem('Transactions', JSON.stringify(Transactions.value));

}

</script>