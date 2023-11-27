<template>
    <div class="flex justify-start flex-col text-lg font-semibold p-3">
        <p>Your Balance:</p>
        <p>{{ balance }}</p>
    </div>
</template>

<script setup lang="ts">

const props = defineProps({
    balance: {
        type: Number,
        required: true,
        default: 0
    }
})

</script>
