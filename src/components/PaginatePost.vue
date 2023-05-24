<script setup>
defineProps(['inicio', 'fin','tamaño'])
const emit = defineEmits(['next', 'prev']);
</script>
<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button 
            :disabled="inicio === 0" 
            type="button" 
            @click="emit('prev')" 
            class="btn btn-outline-primary">Previus {{ inicio }}
        </button>
        
        <button :disabled="fin >=tamaño"
                 type="button" 
                 @click="emit('next')" 
                 class="btn btn-outline-primary">Next {{ fin }} 
        </button>
    </div>
</template>