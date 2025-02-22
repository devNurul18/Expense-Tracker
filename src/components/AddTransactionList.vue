<script setup>
    import { ref } from 'vue';
    //emit send event from child to parent
    //Emit trigger parent event listeners
    const emit = defineEmits(['add'])

    const title =  ref('');
    const amount = ref('');
    const type = ref('');

    const errorMessages = ref('')

    //Use condition for valid data
    const TransactionAddNew = () =>{
        if(!title.value || !amount.value || amount.value <= 0){
           errorMessages.value = "Please enter a valid title and positive number";
           return;
        }

        errorMessages.value = '';

        emit ('add' , {
            title: title.value,
            amount: parseFloat(amount.value),
            type: type.value,
        })

         // Reset form fields
        title.value = '';
        amount.value = '';

    }


</script>

<template>

    <div class="mt-4 bg-body-secondary text-center p-4 border border-1 rounded">

        <div v-if="errorMessages" class="alert alert-danger">{{ errorMessages }}</div>

    <div class="d-flex">
            <div class="p-3 col-md-4">
            <input v-model="title" type="text" placeholder="Title" class="form-control form-control-lg" />
            </div>
          <div class="p-3 mb-3 col-md-4">
            <input v-model="amount" type="number" placeholder="Amount"  value="0" class="form-control form-control-lg" />
         </div>
          <div class="p-3 mb-3 col-md-4" >
            <select class="form-select form-control-lg" v-model="type">
                <option value="" selected>Select Type</option>
                <option value="INCOME">Income</option>
                <option value="EXPENSE">Expense</option>
            </select>
         </div>
        
    </div>
    <button @click="TransactionAddNew" class=" btn btn-primary col-md-3">Add</button>
    </div>

</template>

<style scoped>

</style>