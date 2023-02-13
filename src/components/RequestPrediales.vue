<template>
  <p>Cuenta: {{ cuenta }}</p>
  <div class="loading" v-if="loading" aria-busy="true">Cargando...</div>
  <div class="grid" v-else>
    <div>
      <h6>Vencidos</h6>
      {{ vencidos }}
      <template v-for="(item, index) of vencidos">
        <a href="#"> {{ item.ano }}/{{ item.periodo }}</a>
      </template>
      <div v-if="!vencidos">Sin vencidos</div>
    </div>
    <div>
      <h6>Vigentes</h6>
      {{ vigentes }}
      <template v-for="(item, index) of vigentes">
        <a href="#"> {{ item.ano }}/{{ item.periodo }}</a>
      </template>
      <div v-if="!vigentes">Sin vigentes</div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';

const props = defineProps(['cuenta']);
const loading = ref(true);
const vencidos = ref(null);
const vigentes = ref(null);

const loads = async () => {
  let api = 'https://ovica.finanzas.cdmx.gob.mx/ovica-backend/public/api/v1';

  try {
    vigentes.value = await axios.get(api + '/adeudos/vigente/' + props.cuenta)
      .data;
    console.log('::VIFGENTE:::', vigentes.value);
  } catch {}
  try {
    vencidos.value = await axios.get(api + '/adeudos/vencido/' + props.cuenta)
      .data;
    console.log('VENCIDO:::::', vencidos.value);
  } catch {}
  loading.value = false;
};
loads();
</script>
