<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Por onde estou andando</ion-title>
      </ion-toolbar>    
    </ion-header>
    
    <ion-content>
      <div class="container">
        <h2>Coordenadas</h2>
        <h3>{{ latitude }}</h3>
        <h3>{{ longitude }}</h3>
      <ion-button>Salvar localização</ion-button>
      </div>    
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { defineComponent } from 'vue';
import {Geolocation} from '@capacitor/geolocation';

export default defineComponent({
  name: 'Home',
  data () {
    return {
      latitude: 0,
      longitude: 0,
    }
  },
  ionViewWillEnter () {
    this.printCurrentPosition()
  },
  methods: {
     printCurrentPosition: async function() {
      const coordinates = await Geolocation.getCurrentPosition(); 
      console.log('Current positio: ', coordinates);

    this.latitude = coordinates.coords.latitude;
    this.longitude = coordinates.coords.longitude;
    }
  },
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar
  }
});
</script>

<style scoped>
.container {
  background: azure;
}
</style>