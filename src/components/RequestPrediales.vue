<template>
  <p>Cuenta: {{ cuenta }}</p>
  <div class="loading" v-if="loading" aria-busy="true">Cargando...</div>
  <div class="grid">
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
const vigentes = ref([]);

const loads = async () => {
  let api = 'https://ovica.finanzas.cdmx.gob.mx/ovica-backend/public/api/v1';
  const dataVen = null;
  const dataVig = null;
  try {
    dataVen = await axios.get(api + '/adeudos/vencido/' + props.cuenta);
  } catch {}
  try {
    dataVig = await axios.get(api + '/adeudos/vigente/' + props.cuenta);
  } catch {}
  loading.value = false;
  if (dataVen) {
    vencidos.value = dataVen.data;
  }
  if (dataVig) {
    vigentes.value = dataVig.data;
  }
  console.log(loading.value);
};
loads();
</script>
