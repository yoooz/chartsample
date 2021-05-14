<template>
  <canvas ref="chart"></canvas>
</template>

<script>
import { Chart, registerables } from "chart.js";
Chart.register(...registerables);

export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  mounted() {
    const labels = [
      ["東京本社", "123人"],
      ["札幌営業所", "23人"],
      ["仙台営業所", "13人"],
      ["大阪営業所", "65人"],
      ["福岡営業所", "65人"],
      ["那覇営業所", "10人"]
    ];

    const data = {
      labels: labels,
      datasets: [
        {
          label: "Data A",
          data: [70, 80, 80, 70, 70, 80, 70, 70, 80, 70],
          backgroundColor: "rgb(0, 123, 177)"
        },
        {
          label: "Data B",
          data: [40, 50, 40, 50, 40, 40, 40, 50, 40, 50],
          backgroundColor: "rgb(74, 136, 162)"
        },
        {
          label: "Data C",
          data: [40, 50, 50, 60, 40, 30, 30, 50, 60, 80],
          backgroundColor: "rgb(176, 210, 228)"
        },
        {
          label: "Data D",
          data: [30, 20, 30, 30, 20, 20, 30, 30, 20, 20],
          backgroundColor: "rgb(251, 172, 129)"
        }
      ]
    };

    const config = {
      type: "bar",
      data,
      options: {
        indexAxis: "y",
        animation: {
          duration: 500
        },
        // 積み上げ棒のtopを角丸にする
        elements: {
          bar: {
            borderRadius: 5
          }
        },
        plugins: {
          // タイトルの設定
          title: {
            display: true,
            position: "top",
            align: "start",
            font: {
              size: "18"
            },
            color: "black",
            text: "グラフタイトル",
            // topとbottomしか設定できないので↓スペースで調整してる↑
            padding: {
              top: 60,
              bottom: 4
            }
          },
          // 凡例の非表示
          legend: {
            display: false
          }
        },
        scales: {
          x: {
            stacked: true
          },
          y: {
            stacked: true,
            // y軸の目盛軸を非表示にする
            grid: { drawBorder: false },
            // y軸を0始まりにする
            min: 0
          }
        }
      }
    };
    new Chart(this.$refs.chart, config);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
