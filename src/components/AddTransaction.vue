<template>
    <div class="flex justify-start flex-col p-3 bg-white">
        <div class="text-lg font-semibold border-b-2 border-gray-500">
            Add Transaction
        </div>
        <div class="flex justify-center pt-3">
            <div class="flex flex-wrap justify-between w-1/2">
                <div class="flex items-center">
                    <input checked id="default-radio-2" type="radio" v-model="formValue.type" value="INC"
                        name="default-radio" class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300">
                    <label for="default-radio-2" class="ms-2 text-sm font-medium text-green-900">Income</label>
                </div>
                <div class="flex items-center ">
                    <input id="default-radio-1" type="radio" v-model="formValue.type" value="EXP" name="default-radio"
                        class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300">
                    <label for="default-radio-1" class="ms-2 text-sm font-medium text-red-900">Expense</label>
                </div>
            </div>
        </div>
        <div class="flex justify-center pt-3">
            <form @submit.prevent="addTransaction">
                <div class="grid gap-6 mb-6 md:grid-cols-2">
                    <div>
                        <label for="item_text"
                            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Text</label>
                        <input type="text" id="item_text" v-model="formValue.text"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg block w-full p-2.5 "
                            required>
                    </div>
                    <div>
                        <label for="amount"
                            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Amount</label>
                        <input type="number" id="amount" v-model="formValue.amount" min="0" step=".01"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg block w-full p-2.5 "
                            required>
                    </div>
                </div>
                <button type="submit"
                    class="text-white bg-blue-700 hover:bg-blue-800 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center ">Add</button>
            </form>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useToast } from "vue-toastification";

const emit = defineEmits(["addTransaction"]);
const formValue = ref({
    text: "",
    amount: 0,
    type: "INC"
})
const toast = useToast();

const addTransaction = () => {
    if (formValue.value.text && formValue.value.amount) {
        let transData = {
            text: formValue.value.text,
            amount: formValue.value.amount,
            type: formValue.value.type
        }
        emit("addTransaction", transData);

        formValue.value = {
            text: "",
            amount: 0,
            type: "INC"
        }
        console.log("ok")
    } else {
        toast.error("Please fill text and amount");
    }
}
</script>