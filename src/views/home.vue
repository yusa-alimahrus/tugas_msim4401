<template>
    <ion-page>
      <ion-header>
        <ion-toolbar>
          <ion-title>Cryptocurrency List</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content>
        <ion-list>
          <ion-item v-for="crypto in cryptos" :key="crypto.id">
            <ion-label>
              <h2>{{ crypto.name }} ({{ crypto.symbol }})</h2>
              <p>Price: ${{ crypto.price_usd }}</p>
            </ion-label>
          </ion-item>
        </ion-list>
      </ion-content>
    </ion-page>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        cryptos: []
      }
    },
    methods: {
      async fetchCryptos() {
        try {
          const response = await axios.get('https://api.coinlore.net/api/tickers/');
          this.cryptos = response.data.data;
        } catch (error) {
          console.error(error);
        }
      }
    },
    created() {
      this.fetchCryptos();
    }
  }
  </script>
  
  <style>
  ion-list {
    margin: 20px;
  }
  ion-item {
    margin-bottom: 10px;
  }
  </style>
  