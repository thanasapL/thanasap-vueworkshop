<template>
  <h1 class="font-black mb-3">Devices</h1>
  <div class="grid grid-cols-3 gap-4 border border-black ml-0 mr-5 p-3">
    <ul class="border border-gray" v-for="d in devices" :key="d.id">
      <li>
        <router-link :to="{ name: 'device', params: { id: d.id } }"
          ><img :src="d.Photo"
        /></router-link>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Devices',
  props: {
    manufacturerId: Number,
  },
  data() {
    return {
      devices: [
        { id: 1, DeviceName: 'Asus ROG' },
        { id: 2, DeviceName: 'Dell XP13' },
      ],
    };
  },
  watch: {
    manufacturerId: function (newId, oldId) {
      // console.log('prop changed:: ', newId, '| ', oldId);
      this.validateId(newId);
    },
  },
  created() {
    // console.log('Prop ::: ', this.manufacturerId);
    this.validateId(0);
  },
  methods: {
    validateId(id) {
      let uri = 'https://demo.yume-dev.me/devices';
      if (id != 0 || id) {
        uri = `${uri}?ManufacturerID=${id}`;
        // console.log('URI :: ', uri);
        this.getDevices(uri);
      } else {
        this.getDevices(uri);
      }
    },
    getDevices(uri) {
      axios.get(uri).then((res) => {
        // console.log('Devices: ', res.data);
        this.devices = res.data;
      });
    },
  },
};
</script>
