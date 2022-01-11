<template>
  <div class="container text-center">
    <h1>Device ID : {{ id }}</h1>
    <p>----------------------</p>
    <p>{{ device.Title }}</p>
    <p>{{ device.Processor }}</p>
    <p>Price : ${{ device.Price }}</p>
    <img class="block mx-auto" :src="device.Photo" />
  </div>
  <router-link to="/" class="grid grid-cols-4"
    ><div
      class="
        col-start-2 col-end-4
        rounded
        text-center
        p-2
        bg-green-500
        hover:bg-green-400
      "
    >
      Home
    </div></router-link
  >
</template>

<script>
import { computed } from 'vue';
import { useRoute } from 'vue-router/dist/vue-router.esm-bundler';
import axios from 'axios';
export default {
  name: 'detail',
  setup() {
    const route = useRoute();
    const id = computed(() => route.params.id);
    return {
      id,
    };
  },
  data: () => ({
    device: [
      {
        Title: '',
        Processor: '',
        Photo: '',
        Price: '',
      },
    ],
  }),
  created() {
    axios.get(`https://demo.yume-dev.me/devices?id=${this.id}`).then((res) => {
      [this.device] = res.data;
      // console.log(this.device);
    });
  },
};
</script>
