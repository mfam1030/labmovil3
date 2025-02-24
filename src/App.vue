<template>
  <div class="contenedor-conversor">
    <h1>Conversor de Temperatura</h1>
    <div class="grupo-entrada">
      <input v-model="temperatura" type="number" placeholder="Ingresa la temperatura" class="entrada-temperatura" />
      <select v-model="unidadOrigen" class="seleccion-unidad">
        <option value="Celsius">Celsius</option>
        <option value="Fahrenheit">Fahrenheit</option>
        <option value="Kelvin">Kelvin</option>
      </select>
      <span class="texto-a">a</span>
      <select v-model="unidadDestino" class="seleccion-unidad">
        <option value="Celsius">Celsius</option>
        <option value="Fahrenheit">Fahrenheit</option>
        <option value="Kelvin">Kelvin</option>
      </select>
      <button :disabled="!formularioValido" @click="convertirTemperatura" class="boton-convertir">Convertir</button>
    </div>
    <div v-if="temperaturaConvertida !== null" class="resultado">
      <p>{{ temperatura }} {{ unidadOrigen }} son {{ temperaturaConvertida.toFixed(2) }} {{ unidadDestino }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      temperatura: null,
      unidadOrigen: 'Celsius',
      unidadDestino: 'Fahrenheit',
      temperaturaConvertida: null
    };
  },
  computed: {
    formularioValido() {
      return this.temperatura !== null && this.unidadOrigen && this.unidadDestino;
    }
  },
  methods: {
    convertirTemperatura() {
      let temp = parseFloat(this.temperatura);
      if (this.unidadOrigen === 'Celsius') {
        if (this.unidadDestino === 'Fahrenheit') {
          this.temperaturaConvertida = (temp * 9/5) + 32;
        } else if (this.unidadDestino === 'Kelvin') {
          this.temperaturaConvertida = temp + 273.15;
        } else {
          this.temperaturaConvertida = temp;
        }
      } else if (this.unidadOrigen === 'Fahrenheit') {
        if (this.unidadDestino === 'Celsius') {
          this.temperaturaConvertida = (temp - 32) * 5/9;
        } else if (this.unidadDestino === 'Kelvin') {
          this.temperaturaConvertida = (temp - 32) * 5/9 + 273.15;
        } else {
          this.temperaturaConvertida = temp;
        }
      } else if (this.unidadOrigen === 'Kelvin') {
        if (this.unidadDestino === 'Celsius') {
          this.temperaturaConvertida = temp - 273.15;
        } else if (this.unidadDestino === 'Fahrenheit') {
          this.temperaturaConvertida = (temp - 273.15) * 9/5 + 32;
        } else {
          this.temperaturaConvertida = temp;
        }
      }
    }
  }
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f9;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

.contenedor-conversor {
  background: white;
  padding: 2rem;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  text-align: center;
  max-width: 400px;
  width: 100%;
}

h1 {
  margin-bottom: 1.5rem;
  color: #333;
}

.grupo-entrada {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.entrada-temperatura, .seleccion-unidad, .boton-convertir {
  padding: 0.75rem;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 1rem;
}

.entrada-temperatura {
  width: 100%;
}

.seleccion-unidad {
  width: 100%;
  background-color: #fff;
}

.boton-convertir {
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.boton-convertir:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

.boton-convertir:hover:not(:disabled) {
  background-color: #0056b3;
}

.texto-a {
  font-size: 1rem;
  color: #555;
}

.resultado {
  margin-top: 1.5rem;
  font-size: 1.2rem;
  color: #333;
}
</style>