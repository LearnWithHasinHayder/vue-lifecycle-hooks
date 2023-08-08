<script setup>
import { ref, onMounted, shallowRef, computed, onUpdated, onBeforeMount, watch, watchEffect, nextTick } from 'vue';
const newItem = ref(16)
let chart = null

// const dataset = shallowRef([
//   300, 50, 100
// ])

const dataset = ref([
  300, 50, 100
])

watch(()=>[...dataset.value], (newVal, oldVal) => {
  chart.data.datasets[0].data = newVal
  chart.update()
})

function getDataSet(){
  return dataset.value
}
const data = {
  labels: [
    'Red',
    'Blue',
    'Yellow'
  ],
  datasets: [{
    label: 'My First Dataset',
    data: [],
    backgroundColor: [
      'rgb(255, 99, 132)',
      'rgb(54, 162, 235)',
      'rgb(255, 205, 86)',
      'rgb(43, 105, 86)',
      'rgb(21, 21, 186)',
    ],
    hoverOffset: 4
  }]
};

const config = {
  type: 'pie',
  data: data,
};

onMounted(() => {
  const ctx = document.getElementById('chart')
  chart = new Chart(ctx, config);
  chart.data.datasets[0].data = Object.assign([], getDataSet())
})

function updateChart() {
  dataset.value.push(newItem.value)
  // chart.data.datasets[0].data = getDataSet()
  // chart.update()
}
</script>

<template>
  <div class=" mx-auto w-[400px] h-[400px] bg-gray-400">
    <canvas id="chart">
    </canvas>
  </div>

  <div class="mt-20">
    <input type="text" v-model="newItem">
    <button @click="updateChart()" class="ml-2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
      Button
    </button>

  </div>
</template>

<style scoped></style>
