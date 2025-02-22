<script setup>
    import { ref, computed } from 'vue';
    //Get the data from app folder
    const props = defineProps (['transactions']);

    //delete event will trigged from parent component
    const emit = defineEmits(['delete']);

    const filterType = ref('all');

    //Computed property For Filtered transactions
    const filteredTransactions = computed(() =>{
        if (filterType.value == 'income'){
            return props.transactions.filter(t => t.type.toLowerCase() === 'income');
        }else if (filterType.value === 'expense'){
            return props.transactions.filter (t => t.type.toLowerCase() === 'expense');
        }

        return props.transactions;
    })

</script>

<template>

    <div class="mt-4">

        <div class="mb-3 d-flex gap-4">
            <div>
                <label for="all-filter" class="fw-bold">All</label>
                <input type="radio" name="type" class="form-check-input mx-1" value="all" v-model="filterType" />
            </div>
           
            <div>
                <label for="filter-for-income" class="fw-bold">Income</label>
                <input type="radio" name="type" class="form-check-input mx-1" value="income" v-model="filterType">
            </div>
            <div>
                <label for="filter-for-expense" class="fw-bold">Expense</label>
                <input type="radio" name="type" class="form-check-input mx-1" value="expense" v-model="filterType">
            </div>
           
        </div>

        <!-- If transaction is empty no data will show table will not render -->
        <table class="table table-bordered text-center">
            <thead>
                <tr>
                    <th>Title</th>
                    <th>Amount</th>
                    <th>Type</th>
                    <th>Actions</th>
                </tr>
            </thead>
                <tbody>
                    <tr v-for="(item, index) in filteredTransactions" :key="index">
                        <td>{{ item.title }}</td>
                        <td :class="{'text-success fw-bold' : item.type === 'INCOME' , 'text-danger ' : item.type === 'EXPENSE' , 'text-danger fw-bold' : item.amount >= 500}">${{ item.amount }}                           
                        </td>
                        <td class="text-primary text-uppercase">{{ item.type }}</td>
                        <td><button @click="$emit('delete' , index)" class="btn btn-danger w-100">Delete</button></td>
                    </tr>
                    
                </tbody>
                
        </table>
        <p v-if="props.transactions.length === 0 " class="text-center text-muted" >No transactions record yet.</p>
    </div>
    
</template>

<style scoped>

</style>
