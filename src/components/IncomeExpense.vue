<template>
    <div class="flex gap-x-1 text-lg font-semibold p-3">
        <div class="bg-green-200 rounded-sm p-2 w-1/2">
            <p>Income</p>
            <p>{{ income }}</p>
        </div>
        <div class="bg-red-300 rounded-sm p-2 w-1/2">
            <p>Expense</p>
            <p>{{ expense }}</p>
        </div>
    </div>
</template>

<script setup lang="ts">

const props = defineProps({
    income: {
        type: Number,
        required: true,
        default: 0
    },
    expense: {
        type: Number,
        required: true,
        default: 0
    }
})

</script>