<script setup>
import { ref } from "vue";
import PieChart from "./PieChart.vue";



const data = ref({
});

const dataList = [
  {
    labels: ['첫구매', '여러번구매'],
    datasets: [
      {
        backgroundColor: ['#ffcf9f', '#9acff5', '#d7acd5', '#dbedec'],
        data: [30, 80]
      }
    ]
  },
  {
    labels: ['PC', 'Mobile'],
    datasets: [
      {
        backgroundColor:  ['#9acff5', '#d7acd5'],
        data: [40, 25]
      }
    ]
  },
  {
    labels: ['이게', '뭐지'],
    datasets: [
      {
        backgroundColor:  [ '#d7acd5', '#dbedec'],
        data: [660, 8000]
      }
    ]
  }
];

const setData = (no) => {
  data.value =dataList[no];
}

setData(0);

</script>

<template>
  <div>
    <nav>
    <a class="button" @click="setData(0)">0</a>
    /<a class="button" @click="setData(1)">1</a>
    /<a class="button" @click="setData(2)">2</a>
    </nav>
    <div style="max-width:500px; min-width:100px">

    <PieChart :data="data"/>
    </div>
  </div>
</template>
