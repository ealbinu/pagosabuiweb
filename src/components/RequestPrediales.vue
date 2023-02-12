<template>
  <p>Cuenta: {{ cuenta }}</p>
  <template v-for="(item, index) from vencidos">
    <a href="#"> {{ item.ano }}/{{ item.periodo }}</a>
  </template>
</template>

<script setup>
import axios from 'axios';
const props = defineProps(['cuenta']);
const vencidos  = []

const loads = async () => {
  vencidos = await axios.get(
    'https://ovica.finanzas.cdmx.gob.mx/ovica-backend/public/api/v1/adeudos/vencido/' +
      props.cuenta
  );
}

loads ();
</script>
