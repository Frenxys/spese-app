<template>
  <div class="chart-container">
    <h2 class="chart-title">Distribuzione delle Spese</h2>

    <!-- Grafico a torta -->
    <div class="pie-chart">
      <canvas id="myPieChart"></canvas>
    </div>
  </div>
</template>

<script>
// Importa gli elementi necessari da Chart.js
import { Chart as ChartJS, Title, Tooltip, Legend, ArcElement, PieController } from "chart.js";

// Registra i componenti necessari per il grafico
ChartJS.register(Title, Tooltip, Legend, ArcElement, PieController);

export default {
  name: "ExpensesChart",
  props: {
    spese: Array  // Ricevi le spese come prop
  },
  data() {
    return {
      chartData: {
        labels: this.spese.map(spesa => spesa.motivo),
        datasets: [
          {
            data: this.spese.map(spesa => spesa.importo),
            backgroundColor: ["#FF6384", "#36A2EB", "#FFCE56", "#FF9F40", "#4BC0C0"],
            hoverBackgroundColor: ["#FF6384", "#36A2EB", "#FFCE56", "#FF9F40", "#4BC0C0"]
          }
        ]
      }
    };
  },
  mounted() {
    this.$nextTick(() => {
      new ChartJS(document.getElementById('myPieChart'), {
        type: 'pie',  // Tipo di grafico (torta)
        data: this.chartData,
        options: {
          responsive: true,
          plugins: {
            legend: {
              position: 'top',
            }
          }
        }
      });
    });
  }
};
</script>

<style scoped>
/* Stilizzazione per la pagina del grafico */
.chart-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.pie-chart {
  width: 300px;
  height: 300px;
  margin-bottom: 20px;
}
</style>
