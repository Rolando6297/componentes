<script setup>
    import { ref } from 'vue';
    const counter = ref(0);
    const increment = () => counter.value ++;
    increment()
</script>

<template>
    <button class="btn btn-success">Counter</button>
    <button class="btn btn-secondary">{{ counter }}</button>
</template>

<style >

</style>