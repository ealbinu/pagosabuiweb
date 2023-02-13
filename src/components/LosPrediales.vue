<template>
  <h2>Prediales</h2>
  <div class="grid">
    <template v-for="(item, index) in inmuebles">
      <article class="predial">
        <h5>{{ item.nombre }}</h5>
        <RequestPrediales :cuenta="item.cuenta" />
      </article>
    </template>
  </div>
</template>
<script setup>
import RequestPrediales from './RequestPrediales.vue';
const inmuebles = [
  { nombre: 'Morelos #334', cuenta: '023430140006' },
  { nombre: 'Morelos #336', cuenta: '023430130007' },
  { nombre: 'Morelos #338', cuenta: '023430360000' },
  { nombre: 'Luis L Pardo #31', cuenta: '023542190006' },
  { nombre: 'Granados #44', cuenta: '008130240008' },
  { nombre: 'Isabel #486', cuenta: '008122180006' },
];
</script>
