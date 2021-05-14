<template>
  <v-container>
    <canvas ref="chart"></canvas>
    <v-simple-table>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">
              グループ合計
            </th>
            <th class="text-left">
              一人あたりの1日平均
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in desserts" :key="item.name">
            <td style="height: 60px; text-align: center;">{{ item.name }}</td>
            <td style="height: 60px; text-align: center;">
              {{ item.calories }}
            </td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </v-container>
</template>

<script>
import { Chart, registerables } from "chart.js";

Chart.register(...registerables);

export default {
  name: "Chart",
  data() {
    return {
      desserts: [
        {
          name: "39,300h",
          calories: "8h12m"
        },
        {
          name: "39,300h",
          calories: "8h12m"
        },
        {
          name: "39,300h",
          calories: "8h12m"
        },
        {
          name: "39,300h",
          calories: "8h12m"
        },
        {
          name: "39,300h",
          calories: "8h12m"
        },
        {
          name: "39,300h",
          calories: "8h12m"
        }
      ]
    };
  },
  mounted() {
    const labels = [
      ["GroupA", "123人"],
      ["GroupB", "23人"],
      ["GroupC", "13人"],
      ["GroupD", "65人"],
      ["GroupE", "65人"],
      ["GroupF", "10人"]
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
        responsive: true,
        maintainAspectRatio: false,
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

<style>
div.container {
  height: 500px;
}
.v-data-table {
  position: absolute;
  top: 46px;
  right: 100px;
  margin-top: 4px;
  width: 200px;
  border-right: solid 1px;
  border-left: solid 1px;
  border-color: #808080;
}
</style>
