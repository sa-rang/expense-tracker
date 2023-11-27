
<template>
  <main class="flex justify-center">
    <div class="bg-orange-100 p-3 lg:w-[400px]">
      <Header />
      <Balance :balance="totals.balance" />
      <IncomeExpense :income="totals.income" :expense="totals.expense" />
      <TransactionList :transactions="transactions" @deleteTransaction="handleDelete" />
      <AddTransaction @addTransaction="handleTansaction" />
    </div>
  </main>
</template>

<script setup lang="ts">
import Header from '../components/Header.vue'
import Balance from '../components/Balance.vue'
import IncomeExpense from '../components/IncomeExpense.vue'
import TransactionList from '../components/TransactionList.vue'
import AddTransaction from '../components/AddTransaction.vue'
import { ref, computed, onMounted } from "vue"
import { useToast } from "vue-toastification";

interface Transaction {
  id: string,
  text: string,
  amount: number,
  type: string
}

const toast = useToast();

const transactions = ref<Transaction[]>([])
onMounted(() => {
  const savedTrans = localStorage.getItem('transactions')
  if (savedTrans) {
    transactions.value = JSON.parse(savedTrans);
  }

})

//calculate Balance,Income,Expense
const totals = computed(() => {
  let expense = 0;
  let income = 0;
  transactions.value.map((each) => {
    if (each.type == "INC") {
      income = income + each.amount
    } else {
      expense = expense + each.amount
    }
  })

  return { balance: income - expense, income, expense }
})
const handleTansaction = (iData: Transaction) => {
  transactions.value.push(
    {
      ...iData,
      id: generateId(),
    }
  )
  saveToLocalStorage()
  toast.success("Transaction added!");
}

const handleDelete = (id: string) => {
  transactions.value = transactions.value.filter((t) => t.id != id)
  saveToLocalStorage()
  toast.success("Transaction deleted!");
}

const saveToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}

const generateId = (
  length = 5,
  characters = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz'
) =>
  Array.from(crypto.getRandomValues(new Uint32Array(length)))
    .map((x) => characters[x % characters.length])
    .join('')
</script>