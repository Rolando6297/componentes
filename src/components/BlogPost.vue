<script setup>
//const props = defineProps(['titulo', 'id', 'body', 'color']);
// code alt+shif+f  ctrl+shift+ñ terminal ctrl+shift+i  ctrl +d buscar coincidncia
defineProps({
    title:String,
    id: Number,
    body: {
        type: String,   
        default:"Sin desccripcion",
    },
    color: {
        type: String,
        default: "success"
    },
});
const emit = defineEmits ([
    'cambiarFavEmit'
])

</script>
<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title" :class="`text-${color}`">{{ id }} {{ title }} </h5>
            <p>Lorem ipsum dolor {{ body }}</p>
            <button @click="emit('cambiarFavEmit', title)" class="btn btn-outline-success"  > Favorite</button>
        </div>

    </div>
</template>