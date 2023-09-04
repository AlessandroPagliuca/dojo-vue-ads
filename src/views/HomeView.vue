<template>
  <div class="container wrapper color-white">
    <!-- NAVBAR -->
    <nav class="d-flex justify-content-between py-3">
      <!-- LOGO AND TITLE -->
      <div class="d-flex align-items-center cursor-logo">
        <i class="fa-brands fa-spotify display-4"></i>
        <h1 class="fw-semibold ps-1">Spotify</h1>
      </div>
      <!-- TAG COOKIE E SESSION -->
      <div class="d-flex align-items-center fw-semibold">
        <a href="#">Cookie</a>
        <span class="px-3">|</span>
        <a href="#">Session</a>
      </div>
    </nav>
    <!-- CONTENT -->
    <div class="d-flex flex-column align-items-start py-5">
      <h2 class="fw-semibold display-1">Passa a Premium gratis per 1 mese</h2>
      <span class="fw-semibold py-4">Al termine dell'offerta, solo € 9,99 al mese. Annulla in qualsiasi momento</span>
      <button class="btn btn-bg text-uppercase rounded-5 py-3 px-5">vedi i piani</button>
      <small class="pt-4">Si applicano Termini e condizioni. L'offerta di 1 mese gratis non è disponibile per gli utenti
        che hanno già
        provato Spotify Premium.</small>
    </div>
  </div>
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

<style lang="scss" scoped>
@use '../assets/partials/variables' as *;

.wrapper {
  width: 100%;
  height: 100vh;
}

.color-white {
  color: $white;
}

.btn-bg {
  background-color: $black;
  color: $white;

  &:hover {
    background-color: rgb(40, 40, 40);
    color: beige;

  }
}

a {
  text-decoration: none;
  color: inherit;
  /* Eredità del colore del testo dalla classe padre */
  cursor: pointer;

  &:hover {
    color: beige;
  }
}

.cursor-logo {
  cursor: pointer;

  &:hover {
    color: beige;
  }
}
</style>

