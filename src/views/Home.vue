<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Calc Raíz</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Calc Raíz</ion-title>
        </ion-toolbar>
      </ion-header>
    
      <div id="container">
        <form @submit.prevent="calculo">
          <div>
              <label>Calcular o quadrado do número: </label>
          </div>
          <input v-model.number="num1" type="number"/>
           <ion-button type="submit">Calcular</ion-button>
        </form>
        <div>
          <label>Resultado: {{ resultado }}</label>
        </div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Home',
  data () {
    return {
      num1: '',
      resultado: ''
    }
  },
  methods: {
    calculo () {
      const { resultado, num1 } = this;
      this.resultado = (num1 * num1);
      console.log(resultado);
      
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
#container {
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);

}

form {
  border: 1px solid #8c8c8c;
  border-radius: 3px;
  margin: 0 35% 1%;
  padding: 25px;
}

input {
  margin: 5px;
  width: 80px;
  height: 40px;
  border: 0px;
  border-bottom: 1px solid #8c8c8c;
}

button {
  background-color: blue;
  color: aliceblue;
  width: 100px;
  font-size: 14px;
  padding: 5px 0;
  border-radius: 3px;
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>