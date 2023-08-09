<script setup>
import { ref, onMounted } from 'vue';
const newItem = ref(16)

let chart = null

const dataset = [
  300, 50, 100
]

const data = {
  labels: [
    'Red',
    'Blue',
    'Yellow'
  ],
  datasets: [{
    label: 'My First Dataset',
    data: dataset,
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
  chart = new Chart(ctx, config)
})

function updateChart() {
  dataset.push(newItem.value)
  chart.data.datasets[0].data = dataset
  chart.update()
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
      Add
    </button>

  </div>
</template>

<style scoped></style>
