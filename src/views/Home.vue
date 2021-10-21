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
        <ion-button @click="buscaCidade">Buscar cidade</ion-button>
        <h2>{{ cidade }}</h2>
      </div>    
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButton } from '@ionic/vue';
import { defineComponent } from 'vue';
import { Geolocation } from '@capacitor/geolocation';
import { Http } from '@capacitor-community/http';

export default defineComponent({
  name: 'Home',
  data () {
    return {
      latitude: 0,
      longitude: 0,
      cidade: ''
    }
  },
  ionViewWillEnter () {
    this.printCurrentPosition ()
  },
  methods: {
     printCurrentPosition: async function () {
      const coordinates = await Geolocation.getCurrentPosition(); 
      console.log('Current positio: ', coordinates);

    this.latitude = coordinates.coords.latitude;
    this.longitude = coordinates.coords.longitude;
    }, 
    buscaCidade: async function () {
      const ACCESS_KEY = '9ac1b50e5e40ddbb1d785e07b9489ac5';
      // let url = 'http://api.positionstack.com/v1/reverse?access_key=' + ACCESS_KEY + '&query=' + this.latidude + ',' + this.longitude;
    
    const options = {
      url: `http://api.positionstack.com/v1/reverse?access_key=${ACCESS_KEY}&query=${this.latitude},${this.longitude}`
    };

    const response = await Http.get(options);
    console.log('resposta recebida', response);

    this.cidade = response.data.data[0].locality + ', ' + response.data.data[0].region_code;
    }
  },
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonButton
  }
});
</script>

<style scoped>
.container {
  background: azure;
}
</style>