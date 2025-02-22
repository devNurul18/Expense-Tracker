<script setup>
    import { ref, watch, onMounted } from 'vue';
    import AddTransactionList from './components/AddTransactionList.vue';
    import TransactionList from './components/TransactionList.vue'

    // //Reactive Transaction array
    const transactions = ref([]);

    //Load from localStorage when the app starts
    onMounted(() =>{
        const storeData = localStorage.getItem('transactions');
        if(storeData) transactions.value = JSON.parse(storeData)
    });

    watch(transactions, (newTransactions) => {
        localStorage.setItem('transactions' , JSON.stringify(newTransactions))
    }, {deep : true});


    //Add a new Transaction 
    const addTransaction = (transaction) => {
        transactions.value.push(transaction);
    }


    //Delete The Transaction -> remove the index number 1 item
    const deleteTransaction = (index) => {
        transactions.value.splice(index, 1)
    }
   
</script>

<template>

    <div class="container mt-5 w-50">
        <h1 class="text-center text-danger">Expense Tracker</h1>
        <add-transaction-list @add="addTransaction"/>
        <transaction-list :transactions="transactions" @delete="deleteTransaction"/>
    </div>

</template>

<style scoped>

   
</style>