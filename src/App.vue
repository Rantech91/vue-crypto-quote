<script setup>
import { ref, reactive } from "vue";
import Alerta from "./components/Alerta.vue";
import Cotizacion from "./components/Cotizacion.vue";
import Spinner from "./components/Spinner.vue";
import useCripto from "./composables/useCripto";

const {
  monedas,
  criptomonedas,
  cargando,
  cotizacion,
  obtenerCotizacion,
  mostrarResultado,
} = useCripto();

const error = ref("");

const cotizar = reactive({
  moneda: "",
  criptomoneda: "",
});

const cotizarCripto = () => {
  //validar que cotizar esta lleno
  //if (!cotizar.moneda || !cotizar.criptomoneda) opcional
  if (Object.values(cotizar).includes("")) {
    error.value = "todos los campos son obligatorios";
    setTimeout(() => {
      error.value = "";
    }, 3000);
    return;
  }
  error.value = "";
  obtenerCotizacion(cotizar);
};
</script>

<template>
  <div class="contenedor">
    <h1 class="titulo">Cryptocurrency <span>quote</span></h1>
    <div class="contenido">
      <Alerta v-if="error">{{ error }}</Alerta>
      <form class="formulario" @submit.prevent="cotizarCripto">
        <div class="campo">
          <label for="moneda">Currency:</label>
          <select id="moneda" v-model="cotizar.moneda">
            <option value="">-- Select --</option>
            <option :value="moneda.codigo" v-for="moneda in monedas">
              {{ moneda.texto }}
            </option>
          </select>
        </div>
        <div class="campo">
          <label for="cripto">Criptomoneda:</label>
          <select id="cripto" v-model="cotizar.criptomoneda">
            <option value="">-- Select --</option>
            <option
              :value="criptomoneda.CoinInfo.Name"
              v-for="criptomoneda in criptomonedas"
            >
              {{ criptomoneda.CoinInfo.FullName }}
            </option>
          </select>
        </div>
        <input type="submit" value="Cotizar" />
      </form>

      <Spinner v-if="cargando" />

      <Cotizacion v-if="mostrarResultado" :cotizacion="cotizacion" />
    </div>
  </div>
</template>
