<script setup>
import ChartDataLabels from 'chartjs-plugin-datalabels';
import { Chart as ChartJS, ArcElement, Tooltip, Legend } from 'chart.js'
import { Pie } from 'vue-chartjs';

const props = defineProps(['data'])


const randomColor = ['#ffcf9f', '#9acff5', '#d7acd5', '#dbedec'];

// const data = {
//   labels: ['PC', 'Mobile'],
//   datasets: [
//     {
//       backgroundColor: randomColor.sort(() => Math.random() - 0.5),
//       data: [40, 25]
//     }
//   ]
// }

const options = {
  responsive: true,
  aspectRatio: 1,
  // maintainAspectRatio: false,
  plugins: {
    legend: {
      position: 'bottom',
      labels: {
        usePointStyle: true,
        generateLabels: function(chart) {
          const data = chart.data;
          if (data.labels.length && data.datasets.length) {
            return data.labels.map(function(label, i) {
              const dataset = data.datasets[0];
              const value = dataset.data[i];
              return {
                text: `${label}: ${value}`, // 레이블과 데이터 값을 함께 표시
                fillStyle: dataset.backgroundColor[i],
                hidden: isNaN(dataset.data[i]), // 데이터가 없는 경우 레전드에서 숨김
                index: i,
                fontColor : '#fff'

              };
            });
          }else{
            return {};
          }
        }
      }
    },
    datalabels:{
      color: 'black',
      formatter: function(value, context) {
        const sum = context.chart.data.datasets[0].data.reduce((a,b) => (a+b)) || 0;
        const p =Math.round(value/sum* 100)
        return `${context.chart.data.labels[context.dataIndex]} ${p}%`;
      }
    }

  }
}

ChartJS.register(ArcElement, Tooltip, Legend,ChartDataLabels )

</script>

<template>
  <div>
    {{props.data}}
    <Pie :data="data" :options="options" />
  </div>
</template>
