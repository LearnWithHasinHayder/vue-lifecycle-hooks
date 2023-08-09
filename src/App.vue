<script setup>
import { ref, reactive } from 'vue'
const index = ref(0);
const compositionHooks = [
  'onBeforeMount',
  'onMounted',
  'onBeforeUpdate',
  'onUpdated',
  'onBeforeUnmount',
  'onUnmounted',
  'onErrorCaptured',
]

function nextHook(){
  if(index.value < compositionHooks.length){
    index.value++
  }
}
</script>

<template>
  <section class="mx-auto container">
    <h1 class="mt-10 mb-20">Lifecycle Hooks</h1>

    <h2 class="my-5 text-2xl" v-for="n in index">
      {{ compositionHooks[n - 1] }}
    </h2>

    <button class="">
      <button @click="nextHook()" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
        Next Hook
      </button>
    </button>

  </section>
</template>

<style scoped></style>
