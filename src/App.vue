<template>
  <div class="app-container">
    <!-- Box principale per aggiungere spese -->
    <div class="expense-box">
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

    <!-- Box per la tabella delle spese -->
    <div class="table-box">
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
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      nuovaSpesa: {
        importo: "",
        motivo: ""
      },
      spese: []
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
    }
  }
};
</script>


