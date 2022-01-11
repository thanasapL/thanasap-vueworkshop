<template>
  <div class="grid grid-cols-2 gap-4 border-black">
    <div class="ml-10 mr-0">
      <h1 class="font-black mb-3">Manufacturer</h1>
      <ul class="border border-black" v-for="m in manufacturer" :key="m.id">
        <li>
          <button @click="changeManufacturerId(m.id)">
            <img :src="m.Logo" width="100" />
          </button>
        </li>
      </ul>
    </div>
    <div>
      <slot :factId="currentManufactID"></slot>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Manufacturer',
  data() {
    return {
      currentManufactID: 0,
      manufacturer: [
        { id: 1, Title: 'Asus' },
        { id: 2, Title: 'Dell' },
      ],
    };
  },
  created() {
    this.getManufacturer();
  },
  methods: {
    async getManufacturer() {
      const res = await axios.get('https://demo.yume-dev.me/manufacturers');
      // console.log(res);
      this.manufacturer = res.data;
    },
    changeManufacturerId(id) {
      // console.log('changeManufacturer ::: ', id);
      this.currentManufactID = id;
    },
  },
};
</script>
