<script setup>
import {ref, onBeforeMount, onMounted, onUnmounted, onUpdated } from 'vue'
const status = ref([])
const apiResponse = ref(null)

onBeforeMount(() => {
  console.log('before mount')
  status.value.push('before mount')

  fetch('https://jsonplaceholder.typicode.com/todos/1')
    .then(response => response.json())
    .then(json => {
      apiResponse.value = json
    })
})

// onBeforeMount(function(){
//   status.value.push('before mount')
// })

onMounted(() => {
  console.log('mounted')
  status.value.push('mounted')
})


</script>

<template>
  <section class="mx-auto container">
    <h1 class="my-5">Lifecycle Hooks</h1>
    <div class="flex justify-between mt-20">
      <div class="w-1/2">
        <img src="//vuejs.org/assets/lifecycle.16e4c08e.png" alt="">
      </div>
      <div class="text-2xl w-1/2">
        {{ status }}
      </div>
      <p class="mt-10">
        {{ apiResponse  }}
      </p>
    </div>

  </section>

</template>

<style scoped></style>
