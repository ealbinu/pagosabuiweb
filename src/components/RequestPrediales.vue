<template>
  <p>Cuenta: {{ cuenta }}</p>
  <div class="loading" v-if="loading">Cargando...</div>
  <div class="porpagar">
    <div>
      <h4>Vencidos</h4>
      <!--
      <template v-for="(item, index) of vencidos">
        ><a href="#"> {{ item.ano }}/{{ item.periodo }}</a>
      </template>
      -->
    </div>
    <div>
      <h4>Vigentes</h4>
      <!--
      <template v-for="(item, index) of vencidos">
        ><a href="#"> {{ item.ano }}/{{ item.periodo }}</a>
      </template>
      -->
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';

const props = defineProps(['cuenta']);
const loading = ref(true);
const vencidos = ref([]);

const loads = async () => {
  let api = 'https://ovica.finanzas.cdmx.gob.mx/ovica-backend/public/api/v1';
  const dataVen = await .get(api+'/adeudos/vencido/' + props.cuenta );
  const dataVig = await .get(api+'/adeudos/vigente/' + props.cuenta );
  /*
  axios
    .get(
      'https://ovica.finanzas.cdmx.gob.mx/ovica-backend/public/api/v1/adeudos/vencido/' +
        props.cuenta
    )
    .then((res) => {
      vencidos = res.data;
    })
    .catch((error) => {
      console.log(error.response);
    });
    */
}
</script>
