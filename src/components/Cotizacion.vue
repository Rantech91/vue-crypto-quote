<script setup>
const props = defineProps({
  cotizacion: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <div class="contenedor-resultado">
    <h2>Cotizacion</h2>
    <div class="resultado">
      <img
        :src="`https://cryptocompare.com/${props.cotizacion.IMAGEURL}`"
        alt="imagen cripto"
      />
      <div>
        <p>
          El precio es de: <span>{{ props.cotizacion.PRICE }}</span>
        </p>
        <p>
          Highest price 24h: <span>{{ props.cotizacion.HIGH24HOUR }}</span>
        </p>
        <p>
          Lowest price 24h: <span>{{ props.cotizacion.LOWDAY }}</span>
        </p>
        <p>
          24h change percentage:
          <span>{{ props.cotizacion.CHANGEPCT24HOUR }}</span>
        </p>
        <p>
          Last update <span>{{ props.cotizacion.LASTUPDATE }}</span>
        </p>
      </div>
    </div>
  </div>
</template>
