<template>
  <div class="add-transaction">
    <h4>Add New Transaction</h4>
    <form>
        <label for="text">Text</label>
        <input type="text" id="text" placeholder="Enter text...">
        
        <label for="amount">Amount<br>(negative - expense, positive - income)</label>
        <input type="number" id="amount" placeholder="Enter amount...">
        
        <button type="submit">Add Transaction</button>
    </form>
</div>
</template>