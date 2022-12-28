<script setup>

//Los props se peuden pasar como array o como objeto

//const props =defineProps(['title','id','body','colorText']) 

defineProps({
    title: String,
    id: Number,
    body: {
        type:String,
        default: 'Sin Descripcion'
    }
})

const emitir = defineEmits(['cambiarFavoritoNombre'])


</script>

<template>

    <div class="card">

    <div class="card-body">

        <h5 class="card-title" :class="`text-${colorText}`">{{ id }} - {{ title }}</h5>
        <p>{{body}}</p>
        <button @click="emitir('cambiarFavoritoNombre',title)" class="btn btn-outline-primary">Favorito</button>
    </div>


    </div>

</template>