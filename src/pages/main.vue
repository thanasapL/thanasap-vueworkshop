<template>
  <div class="container">
    <manufacturer v-slot="data">
      <device :manufacturerId="data.factId"></device
    ></manufacturer>
  </div>
</template>

<script>
import Manufacturer from '../components/Manufacturer.vue';
import Device from '../components/Devices.vue';
export default {
  name: 'main',
  components: {
    Manufacturer,
    Device,
  },
};
</script>
