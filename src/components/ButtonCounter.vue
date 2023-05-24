<script setup>
import {ref} from 'vue'
const counter = ref(0)
const calculo = () => counter.value ++
</script>
<template>
    <button @click="calculo">Counter - {{ counter }}</button>
</template>