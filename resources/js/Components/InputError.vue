<script setup>
import { defineProps } from 'vue'

defineProps({
    message: String,
})
</script>

<template>
<div v-show="message">
    <p class="text-sm text-red-600">
        {{ message }}
    </p>
</div>
</template>
