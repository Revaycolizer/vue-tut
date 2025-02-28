<script setup>
import { ref } from "vue";

let data = ref([]);

data.value = Array.from({ length: 10 }, (_, index) => index + 1);
</script>

<template>
    <h1 class="text-red-600">Hello</h1>
    <section class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4">
        <div
            v-for="(number, index) in data"
            :key="index"
            class="p-4 border rounded-lg shadow-md text-center"
        >
            {{ number }}
        </div>
    </section>
</template>
