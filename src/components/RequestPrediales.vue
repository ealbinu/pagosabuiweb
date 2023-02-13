<template>
  <p>Cuenta: {{ cuenta }}</p>
  <div class="loading" v-if="loading" aria-busy="true">Cargando...</div>

  <h6>Vencidos</h6>
  <table>
    <template v-for="(item, index) of vencidos">
      <tr>
        <td>
          <strong>{{ item.ANO }}/{{ item.PERIODO }}</strong>
        </td>
        <td>${{ item.SALDO }}</td>
        <td><a href="#" @click="formato(item)"> Formato</a></td>
      </tr>
    </template>
  </table>
  <div v-if="!vencidos">Sin vencidos</div>

  <article>
    <h6>Vigentes</h6>
    <template v-for="(item, index) of vigentes">
      <tr>
        <td><a href="#" @click="formato(item)">Formato pago</a></td>
      </tr>
      <a href="#"> {{ item.texto_bimestre }}</a>
    </template>
    <div v-if="!vigentes">Sin vigentes</div>
  </article>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';
const api = 'https://ovica.finanzas.cdmx.gob.mx/ovica-backend/public';

const props = defineProps(['cuenta']);
const loading = ref(true);
const vencidos = ref(null);
const vigentes = ref(null);

const loads = async () => {
  try {
    const res = await axios.get(
      api + '/api/v1/adeudos/vigente/' + props.cuenta
    );
    vigentes.value = res.data;

  } catch {}
  try {
    const res = await axios.get(
      api + '/api/v1/adeudos/vencido/' + props.cuenta
    );
    vencidos.value = res.data;

  } catch {}
  loading.value = false;
};
loads();

const formato = async (item) => {
  const res = await axios.patch(api + '/api/v1/adeudos/vencido/liquidacion', {
    adeudos: [{ ...item, checked: true }],
    ctapredial: props.cuenta,
  });
  const formato = await axios.post(api + '/formatos/pago/generaFUT', {
    token: res.data.resumen.lc_token,
  });
  console.log(formato);
  /*
  const res = axios.post('/formatos/pago/generaFUT', {
    token: token,
  });
  */
  console.log(res);
};
</script>
