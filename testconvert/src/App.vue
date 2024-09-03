<template>
  
  <div id="app">
    <header>
      <nav>
        <router-link to="/" active-class="active-link">Главная</router-link>
        <router-link to="/convert" active-class="active-link">Конвертация</router-link>
        <select v-model="baseCurrency" @change="fetchRates">
          <option v-for="currency in currencies" :key="currency" :value="currency">{{ currency }}</option>
        </select>
      </nav>
    </header>
    <router-view :baseCurrency="baseCurrency" :rates="rates"></router-view>
  </div>
  
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      baseCurrency: 'RUB',
      currencies: ['RUB', 'USD', 'EUR'],
      rates: {},
    };
  },
  created() {
    this.fetchRates();
  },
  methods: {
    fetchRates() {
      axios.get(`https://api.exchangerate-api.com/v4/latest/${this.baseCurrency}`)
        .then(response => {
          this.rates = response.data.rates;
        });
    },
  },
};
</script>

