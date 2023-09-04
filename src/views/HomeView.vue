<template>
  test
</template>

<script>
import axios from 'axios';
import { store } from '../store';
export default {
  name: 'HomeView',
  data() {
    return {
      store,
      announcement: null,
    }
  },
  methods: {
    async getData() {
      try {
        const response = await axios.get(`${store.apiUrl}/home`)
        this.annoucement = response.data.result;
        console.log(this.annoucement);
      } catch (error) {
        console.error('Errore nella chiamata API:', error);
      }
    }
  },
  mounted() {
    this.getData();
  }

}
</script>

<style lang="scss" scoped></style>

<!-- blue-1= #4383e2; -->