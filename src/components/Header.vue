<template>
    <div class="flex-col md:flex justify-center items-center relative text-white">
        <h1 class="text-6xl text-center mt-3">Voting Application</h1>
        <p class="flex gap-2 justify-center mt-3 md:absolute md:right-2 md:top-0 items-center">
        connection to server:
        <span class="material-symbols-outlined text-sm mt-0.5" :class="connected ? 'text-green-600' : 'text-red-600'">wifi</span>
    </p>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';
const connected = defineProps();
</script>