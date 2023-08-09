<script setup>
import {ref, onBeforeMount, onMounted, watch, onUnmounted, onUpdated } from 'vue'
const status = ref([])
const apiResponse = ref('')

const watchStatus = ref([])
onBeforeMount(() => {
  console.log('before mount')
  status.value.push('before mount')

  fetch('https://jsonplaceholder.typicode.com/todos/1')
    .then(response => response.json())
    .then(json => apiResponse.value = json.title)

    fetch('https://jsonplaceholder.typicode.com/todos/2')
    .then(response => response.json())
    .then(json => apiResponse.value = json.title)
})

onMounted(() => {
  console.log('mounted')
  status.value.push('mounted')
})

watch(() => apiResponse.value, (newVal, oldVal) => {
  console.log('watch status', newVal, oldVal)
  watchStatus.value.push(newVal)
})

watch(() => [...status.value], (newVal, oldVal) => {
  console.log('watch status', newVal, oldVal)
  watchStatus.value.push(newVal)
})



// onUpdated(() => {
//   console.log('updated')
//   status.value.push('updated')
// })
</script>

<template>
  <section class="mx-auto container">
    <h1 class="my-5">Lifecycle Hooks</h1>
    <div class="flex justify-between mt-20">
      <div class="w-1/2">
        <img src="//vuejs.org/assets/lifecycle.16e4c08e.png" alt="">
      </div>
      <div class="w-1/2">
        {{ status }}
        <p>
          {{ apiResponse }}
        </p>
        <p>
          {{ watchStatus }}
        </p>
      </div>
    </div>

  </section>

</template>

<style scoped></style>
