<template>
  <p>Cuenta: {{ cuenta }}</p>
  <template v-for="(item, index) of vencidos">
    <CoreArrow variant="path" strokeWidth="6" , flip="x"></CoreArrow>
    ><a href="#"> {{ item.ano }}/{{ item.periodo }}</a>
  </template>
</template>

<script setup>
import axios from 'axios';
import { CoreFigma } from '@glyphs/vue-core';

const props = defineProps(['cuenta']);
const vencidos = [];

const loads = async () => {
  console.log('loading...');
  axios
    .get(
      'https://ovica.finanzas.cdmx.gob.mx/ovica-backend/public/api/v1/adeudos/vencido/' +
        props.cuenta
    )
    .then((res) => {
      console.log(res);
      // Handle response
    })
    .catch((error) => {
      console.log(error.response);
    });
};

loads();
</script>
