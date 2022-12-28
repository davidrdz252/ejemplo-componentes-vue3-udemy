<script setup>

const paginas = defineEmits(['siguientepaginanombre','atraspaginanombre'])
const props = defineProps(['inicio','fin','cantidad'])

</script>

<template>


<div class="btn-group" role="group" aria-label="Basic example">
  <button @click="paginas('atraspaginanombre',title)" type="button" class="btn btn-outline-primary" :disabled="inicio <= 0">Atrás</button>
  <button @click="paginas('siguientepaginanombre',title)" type="button" class="btn btn-outline-primary" :disabled="fin >= cantidad">Siguiente</button>

</div>
</template>