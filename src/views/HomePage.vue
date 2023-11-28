<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Tugas 3</ion-title>
      </ion-toolbar>
    </ion-header>  
    <ion-content class="ion-padding">
       <div class='center-button'> 
       <ion-button  @click="toggleDataVisibility">Refresh</ion-button>
       </div>
      <ion-table v-if="showData" class="bordered-table">
        <ion-row class="bordered-custom">
        </ion-row>
        <ion-row v-for="(item, index) in items" :key="item.id">
          <ion-col> RANK <br> <div class="font-index">{{ index + 1 }}</div></ion-col>
          <ion-col>{{ item.name }}<div class="font-index">{{ item.symbol }}</div></ion-col>
          <ion-col>USD <br><div class="font-index">{{ item.price_usd }}</div></ion-col>
        </ion-row>
      </ion-table>
    </ion-content>
  </ion-page>
</template>

<script >
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import axios from 'axios';

export default {
  data() {
    return {
      items: [],
      showData: false,
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      axios.get('https://api.coinlore.net/api/tickers/')
        .then(response => {
          this.items = response.data.data;
        })
        .catch(error => {
          console.error('Error fetching data:', error);
        });
    },
    toggleDataVisibility() {
      this.showData = !this.showData;
    },
  },
};

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

.bordered-custom {
  font-weight: bold;
  font-size: 80%;
}
.font-index {
  font-weight: bold;
  font-size: 130%;
  margin-top: 0.5ch;
}

.bordered-table {
  border-collapse: collapse;
  width: 100%;
}

.bordered-table ion-col {
  border: 1px solid #dddddd;
  text-align: center;
  padding: 10px;
}

.bordered-table ion-row:nth-child(even) {
  background-color: #f2f2f2;
}

.center-button {
  position: relative;
  width: 100%;
  display: flex;
  justify-content: center;
  align-item: center;
  margin-bottom: 1rem;
}
</style>
