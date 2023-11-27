<template>
    <div class="flex flex-col gap-y-1 text-base font-semibold p-3">
        <div v-for="t in transactions" :key="t.id"
            class=" group flex justify-between bg-white rounded-sm p-2 border-l-4 relative"
            :class="t.type == 'INC' ? 'border-green-500' : 'border-red-500'">
            <p>{{ t.text }}</p>
            <p>{{ t.amount }}</p>
            <button @click.prevent="deleteTransaction(t.id)"
                class="hidden group-hover:block bg-red-500 px-2 absolute -right-5 top-2 rounded">X</button>
        </div>
    </div>
</template>

<script setup lang="ts">
const emit = defineEmits(["deleteTransaction"])

defineProps({
    transactions: {
        type: Array,
        required: true
    }
})

const deleteTransaction = (id: String) => {
    emit("deleteTransaction", id)
}

</script>