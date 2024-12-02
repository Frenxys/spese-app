<template>
  <div id="app">
    <h1>Gestione Spese</h1>

    <!-- Form per aggiungere una spesa -->
    <form @submit.prevent="aggiungiSpesa">
      <div>
        <label for="importo">Importo:</label>
        <input v-model="nuovaSpesa.importo" type="number" id="importo" required />
      </div>
      
      <div>
        <label for="motivo">Motivo:</label>
        <input v-model="nuovaSpesa.motivo" type="text" id="motivo" required />
      </div>
      
      <button type="submit">Aggiungi Spesa</button>
    </form>

    <!-- Tabella delle spese -->
    <h2>Spese Giornaliere</h2>
    <table>
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
      // Aggiungi la nuova spesa alla lista
      this.spese.push({
        importo: parseFloat(this.nuovaSpesa.importo),
        motivo: this.nuovaSpesa.motivo
      });

      // Pulisci i campi del form
      this.nuovaSpesa.importo = "";
      this.nuovaSpesa.motivo = "";
    }
  }
};
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}
table, th, td {
  border: 1px solid black;
}
th, td {
  padding: 10px;
  text-align: left;
}
</style>
