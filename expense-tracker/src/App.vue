<script setup>
  import Header from "./components/Header.vue";
  import Balance from "./components/Balance.vue";
  import IncomeExpense from "./components/IncomeExpense.vue";
  import TransactionList from "./components/TransactionList.vue";
  import {ref ,computed} from "vue";
   const transactions = ref([
                    {id: 1,text: 'flower', amount: -19.99},
                    {id: 1,text: 'Salary', amount: -299.99},
                    {id: 1,text: 'flower', amount: -19.99},
                    {id: 1,text: 'bread', amount: 819.99},
                    {id: 1,text: 'Gift', amount: 19.99},
                ]);
  const totalBalance =  computed ( () => {
   return transactions.value.reduce((acc,transaction) => {
    return acc + transaction.amount;
   },0);
  });
  const Income  =  computed ( () => {
   return transactions.value.reduce((acc,transaction) => 
   transaction.amount > 0 ? acc + transaction.amount:acc, 0);
  });
  const Expense  =  computed ( () => {
   return transactions.value.reduce((acc,transaction) => 
   transaction.amount < 0 ? acc + transaction.amount: acc
     ,0);
  });
  
 
</script>
<template>
<Header/>
<div class="container">
<Balance :totalBalance="totalBalance"/>
<IncomeExpense :Income="Income" :Expense="Expense"/>
<TransactionList :transactions="transactions" />
</div>
</template>
