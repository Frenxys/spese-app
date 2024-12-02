<template>
  <div class="app-container">
    <h1 class="app-title">Gestione Spese</h1>

    <!-- Form per aggiungere una spesa -->
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

    <!-- Tabella delle spese -->
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

<style scoped>
/* Contenitore principale */
.app-container {
  font-family: 'Courier New', Courier, monospace;
  background: linear-gradient(45deg, #121212, #2c2f36); /* Nero sfumato con grigio */
  
  padding: 50px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh; /* Fullscreen */
  
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(10px); /* Sfocatura sul background */
}

/* Titolo principale */
.app-title {
  font-size: 3.5rem;
  color: #3e8e41; /* Verde normale */
  margin-bottom: 30px;
  text-shadow: 0 0 10px rgba(62, 142, 65, 0.3);
}

/* Stile del form */
.expense-form {
  background: rgba(44, 47, 54, 0.8); /* Grigio scuro traslucido */
  padding: 25px;
  border-radius: 15px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
  width: 100%;
  max-width: 500px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

/* Campi del form */
.form-group {
  display: flex;
  flex-direction: column;
}

.form-label {
  font-size: 1.4rem;
  color: #4e9f3d; /* Verde scuro */
}

.form-input {
  padding: 12px;
  font-size: 1.2rem;
  color: #fff;
  background-color: #333;
  border: 2px solid #4e9f3d; /* Verde scuro per i bordi */
  border-radius: 10px;
  outline: none;
  transition: all 0.3s ease;
}

.form-input:focus {
  border-color: #3e8e41; /* Verde normale */
  box-shadow: 0 0 10px rgba(62, 142, 65, 0.6);
}

/* Bottone per aggiungere la spesa */
.submit-btn {
  background: linear-gradient(45deg, #4e9f3d, #3e8e41); /* Verde scuro a verde normale */
  color: white;
  padding: 12px 25px;
  border: none;
  border-radius: 10px;
  font-size: 1.3rem;
  cursor: pointer;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
  transition: all 0.3s ease;
}

.submit-btn:hover {
  background: linear-gradient(45deg, #3e8e41, #4e9f3d);
  transform: scale(1.05);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
}

/* Tabella delle spese */
.table-title {
  font-size: 2rem;
  margin-top: 40px;
  color: #fff;
  text-shadow: 0 0 15px rgba(255, 255, 255, 0.2);
}

.expense-table {
  width: 100%;
  max-width: 600px;
  border-collapse: collapse;
  margin-top: 30px;
  background: rgba(44, 47, 54, 0.7); /* Sfondo grigio traslucido */
  border-radius: 15px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
}

.expense-table th,
.expense-table td {
  padding: 15px 20px;
  font-size: 1.2rem;
  text-align: left;
  color: #fff;
}

.expense-table th {
  background: rgba(62, 142, 65, 0.8); /* Verde scuro per l'header */
}

.expense-table tr:nth-child(even) {
  background: rgba(44, 47, 54, 0.9);
}

.expense-table tr:nth-child(odd) {
  background: rgba(44, 47, 54, 0.85);
}

.expense-table tr:hover {
  background-color: rgba(62, 142, 65, 0.3);
  color: #000;
  transition: all 0.3s ease;
}
</style>
