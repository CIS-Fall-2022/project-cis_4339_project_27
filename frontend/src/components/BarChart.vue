<template>
  <canvas ref="myChart"></canvas>
</template>

<script>
import { Chart, registerables } from 'chart.js'

Chart.register(...registerables);
export default {
  props: {
    label: {
      type: Array,
    },
    chartData: {
      type: Array,
    },
  },
  async mounted() {
    console.log(this.chartData);
    await new Chart(this.$refs.myChart, {
      type: "bar",
      data: {
        labels: this.label,
        datasets: [
          {
            label: "Attendance",
            backgroundColor: "rgba(206, 156, 72, 0.65)",
            data: this.chartData,
          },
        ],
      },
      options: {
        scales: {
            y: {
                min: 0,
                
            }
        }
      }
    });
  },
};
</script>