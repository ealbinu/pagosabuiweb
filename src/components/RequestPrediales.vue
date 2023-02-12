<template>
  <p>Cuenta: {{ cuenta }}</p>
</template>

<script setup>
import axios from 'axios';
const props = defineProps(['cuenta']);
</script>
