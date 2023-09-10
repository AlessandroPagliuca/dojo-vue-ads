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
      <button class="btn btn-bg text-uppercase rounded-5 py-3 px-4">vedi i piani</button>
      <small class="pt-4">Si applicano Termini e condizioni. L'offerta di 1 mese gratis non è disponibile per gli utenti
        che hanno già
        provato Spotify Premium.</small>
    </div>
    <!-- Componente Modal -->
    <ModalComp ref="modal" :price="announcement.price" :duration="announcement.duration" :plan="announcement.plan"
      :description="announcement.description" :contract="announcement.contract" />
  </div>
</template>

<script>
import axios from 'axios';
import { store } from '../store';
import ModalComp from '../components/ModalComp.vue';
import Cookies from 'js-cookie';
export default {
  name: 'HomeView',
  components: {
    ModalComp,
  },
  data() {
    return {
      store, //Take apiUrl from the store
      announcement: {
        price: '',
        duration: '',
        plan: '',
        description: '',
        contract: '',
      }
    }
  },
  methods: {
    // Generate a random identifier for the user
    generateRandomId() {
      return Math.random().toString(36).substring(2, 15);
    },
    //temporany function for open modal
    openModal() {
      this.$refs.modal.openModal();
      //chiamo la funzione saveCookie 
      this.saveCookie();
    },
    //funzione asincrona per il salvataggio dei cookie
    async saveCookie() {
      try {
        const value = this.generateRandomId();
        console.log(value, 'prova');
        const announcementId = this.announcement.id;
        Cookies.set('name_cookie', value, { expires: 7 });
        //creazione array dei dati da salvare nel back-end
        const dataCookie = {
          name: 'name_cookie',
          value: encodeURIComponent(value),
          announcement_id: encodeURIComponent(announcementId),
        };

        //chaimata per salvare i cookie nel back-end
        await axios.post(`${store.apiUrl}/cookies/${announcementId}`, dataCookie).then(res => {
          console.log(res.dataCookie, 'success');
        }).catch(error => {
          console.error('Errore durante il salvataggio del cookie:', error);
        });

      } catch (error) {
        console.error('Error saving:', error)
      }
    },
    // Function for call axios to get the annuncement data
    async getData() {
      try {
        const response = await axios.get(`${store.apiUrl}/home`);
        this.announcement = response.data.result;
        this.announcement.id = response.data.result.id; // Assicurati che l'ID dell'annuncio venga ottenuto correttamente
        console.log(this.announcement);
      } catch (error) {
        console.error('API call error:', error);
      }
    }

  },
  // mounted() {
  //   //call of the getData() function to provide the announcement data as soon as we access the site
  //   this.getData();
  //   //call of the openModal() function to display the modal immediately as soon as we access the site
  //   this.openModal();
  // }
  async mounted() {
    try {
      // Aspetta che i dati dell'annuncio vengano ottenuti prima di aprire la modale
      await this.getData();

      // Assicurati che l'annuncio abbia un ID valido prima di salvare il cookie
      if (this.announcement && this.announcement.id) {
        this.openModal();
      } else {
        console.error('ID dell\'annuncio non valido');
      }
    } catch (error) {
      console.error('Errore durante il caricamento dei dati:', error);
    }
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

