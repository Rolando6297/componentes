<script setup>
const emit = defineEmits ([
    'nextPage',
    'prevPage'
])
const props = defineProps(
    [
        "inicio",
        "fin",
        "longitud",
    ]
)


</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" @click="emit('prevPage')"  :disabled="inicio <= 0"  class="btn btn-outline-primary">Previus</button>
        <button type="button" @click="emit('nextPage')" :disabled="fin >= longitud"  class="btn btn-outline-primary">Next</button>
    </div>
</template>