<template>
  <p>Cuenta: {{ cuenta }}</p>
  <div class="loading" v-if="loading" aria-busy="true">Cargando...</div>
  <article>
    <h6>Vencidos</h6>
    <table>
      <template v-for="(item, index) of vencidos">
        <tr>
          <td>{{ item.EJERCICIO }}</td>
          <td>{{ item.PERIODO }}</td>
          <td>{{ item.IMPORTEADEUDO }}</td>
          <td>{{ item.IMPORTEPAGADO }}</td>
          <td><a href="#">Formato de pago</a></td>
        </tr>
      </template>
    </table>
    <div v-if="!vencidos">Sin vencidos</div>
  </article>
  <article>
    <h6>Vigentes</h6>
    <template v-for="(item, index) of vigentes">
      <tr>
        <td><a href="#">Formato pago</a></td>
      </tr>
      <a href="#"> {{ item.texto_bimestre }}</a>
    </template>
    <div v-if="!vigentes">Sin vigentes</div>
  </article>
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
    const res = await axios.get(api + '/adeudos/vigente/' + props.cuenta);
    vigentes.value = res.data;
    console.log('::VIFGENTE:::', vigentes.value);
  } catch {}
  try {
    const res = await axios.get(api + '/adeudos/vencido/' + props.cuenta);
    vencidos.value = res.data;
    console.log('VENCIDO:::::', vencidos.value);
  } catch {}
  loading.value = false;
};
loads();
</script>
