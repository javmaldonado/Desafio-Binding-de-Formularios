<template>
  <div id="app">
    <form>
      <div>
        <label>Título de la tarjeta: </label>
        <input type="text" v-model="titulo">
      </div>

      <div>
        <label>Chip SRC: </label>
        <input type="text" v-model="chip">
      </div>

      <div>
        <label>Número: </label>
        <input type="text" v-model="numero" @input="limitNumero">
      </div>

      <div>
        <label>Fecha de expiración: </label>
        <input type="text" v-model="fecha" @input="formatFecha">
      </div>

      <div>
        <label>Propietario: </label>
        <input type="text" v-model="propietario" @input="limitPropietario">
      </div>

      <div>
        <label>Tipo de tarjeta SRC: </label>
        <input type="text" v-model="tipo">
      </div>
    </form>

    <div class="carnet">
      <h3>{{ titulo }}</h3>
      <img :src="chip" alt="Chip Image" width="40">
      <div>
        <h2>{{ numero }}</h2>
        <span>Fecha exp: <b>{{ formattedFecha }}</b></span>
      </div>
      <footer>
        <span>{{ propietario }}</span>
        <img :src="tipo" width="60" alt="Tipo de Tarjeta" />
      </footer>
    </div>
  </div>
</template>

<script>


export default {
  name: 'BindingForm',
  data() {
    return {
      chip: "",
      tipo: "",
      titulo: "Visa Classic Crédito",
      numero: "",
      fecha: "",
      propietario: "",


    };
  },
  /* Me molestaba que los datos no tuvieran formato/limite por lo que busqué como incorporarlo */
  computed: {
    formattedFecha() {
      return this.fecha.replace(/(\d{2})(\d{2})/, '$1 / $2');
    }
  },
  methods: {
    formatFecha(event) {
      let input = event.target.value.replace(/\D/g, '').substring(0, 4);
      if (input.length >= 2) {
        input = input.substring(0, 2) + ' / ' + input.substring(2, 4);
      }
      this.fecha = input;
    },
    limitPropietario(event) {
      let input = event.target.value;
      if (input.length > 25) {
        input = input.substring(0, 25);
      }
      this.propietario = input;
    },
    limitNumero(event) {
      let input = event.target.value.replace(/\D/g, ''); // Elimina caracteres no numéricos
      if (input.length > 16) { //16 caracteres //
        input = input.substring(0, 16);
      }
      this.numero = input;
    }
  }
};
</script>

<style>
* {
  margin: 0;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 60vh;
  font-size: 10px;
  font-family: sans-serif;
}

#app {
  display: flex;
  gap: 40px;
}

form {
  padding: 18px;
  border-radius: 20px;
  border: ridge 1px;
  box-shadow: 1px 1px 1px 1px gray;
  font-weight: bold;
  display: flex;
  flex-direction: column;
  gap: 15px;
  justify-content: center;
}

form div {
  display: grid;
  grid-template-columns: 100px 200px;
  align-items: center;
  gap: 5px;
}

form div label {
  text-align: right;
}

.carnet {
  width: 400px;
  height: 230px;
  background: #1c1a1e;
  color: white;
  border-radius: 20px;
  padding: 20px;
  box-shadow: 0px 0px 10px 2px black;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

h3 {
  font-size: 20px;
}

h2 {
  font-size: 30px;
  letter-spacing: 10px;
  margin-bottom: 15px;
  text-shadow: 0px 0px 1px gold;
  font-family: Times;
}

b {
  font-size: 16px;
}

footer {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  font-weight: bold;
  font-size: 18px;
  text-transform: uppercase;
  font-style: italic;
}
</style>