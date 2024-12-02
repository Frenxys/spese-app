<template>
  <div class="app-container">
    <!-- Box principale per aggiungere spese -->
    <div v-if="!showChart" class="expense-box">
      <h1 class="app-title">Gestione Spese</h1>
      <form @submit.prevent="aggiungiSpesa" class="expense-form">
        <div class="form-group">
          <label for="importo" class="form-label">Importo</label>
          <input v-model="nuovaSpesa.importo" type="number" id="importo" class="form-input" placeholder="Es. 50" required />
        </div>

        <div class="form-group">
          <label for="motivo" class="form-label">Motivo</label>
          <input v-model="nuovaSpesa.motivo" type="text" id="motivo" class="form-input" placeholder="Es. Pranzo" required />
        </div>

        <button type="submit" class="submit-btn">Aggiungi Spesa</button>
      </form>
    </div>

    <!-- Bottone per passare tra tabella e grafico -->
    <div class="button-container">
      <button @click="toggleView" class="show-chart-btn">
        {{ showChart ? "Mostra Gestione Spese" : "Mostra Grafico" }}
      </button>
    </div>

    <!-- Sezione Tabella Gestione Spese -->
     
    <div  class="table-box">
      <h2 class="table-title">Spese Giornaliere</h2>
      <table class="expense-table">
        
        <thead>
          <tr>
            <th>Importo</th>
            <th>Motivo</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(spesa, index) in spese" :key="index">
            <td>{{ spesa.importo }} €</td>
            <td>{{ spesa.motivo }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- Sezione Grafico -->
    <div v-if="showChart" class="chart-box">
      <expenses-chart :spese="spese" />
    </div>
  </div>
</template>

<script>
// Importa il componente del grafico
import ExpensesChart from './ExpensesChart.vue';

export default {
  name: "App",
  components: {
    ExpensesChart
  },
  data() {
    return {
      nuovaSpesa: {
        importo: "",
        motivo: ""
      },
      spese: [],
      showChart: false // Stato che gestisce la visualizzazione del grafico/tabella
    };
  },
  methods: {
    aggiungiSpesa() {
      this.spese.push({
        importo: parseFloat(this.nuovaSpesa.importo),
        motivo: this.nuovaSpesa.motivo
      });

      this.nuovaSpesa.importo = "";
      this.nuovaSpesa.motivo = "";
    },
    
    // Metodo per alternare la visualizzazione tra grafico e tabella
    toggleView() {
      this.showChart = !this.showChart;
    }
  }
};
</script>

<style scoped>
/* Stilizzazione aggiuntiva per il componente */
.button-container {
  margin: 20px 0;
  text-align: center;
}

.show-chart-btn {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

.show-chart-btn:hover {
  background-color: #45a049;
}

.chart-box {
  text-align: center;
  margin-bottom: 20px;
}

.table-box {
  margin-top: 20px;
}
</style>
