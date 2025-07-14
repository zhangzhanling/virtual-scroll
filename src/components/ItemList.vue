<template>
    <div class="h-10 bg-yellow-100 mt-1 flex justify-center items-center">{{ props.item.name }}</div>
</template>

<script setup>
import { defineProps } from 'vue'
const props = defineProps({
    item: Object
})

</script>