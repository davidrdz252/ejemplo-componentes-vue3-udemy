<script setup>
import {ref} from "vue"
const counter = ref(0)

const increment =  () =>{
  return counter.value++
}

</script>

<template>

<button class="btn btn-primary" @click="increment">Counter {{ counter }}</button>

</template>