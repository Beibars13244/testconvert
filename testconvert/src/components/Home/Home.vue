<template>
  <div>
    <Hero/>
    <h1>Курсы валют на сегодня</h1>
    
    <ul>
      <li v-for="(rate, currency, index) in filteredRates" :key="currency" :class="{ 'first-column': index === 0 }">
        1 {{ baseCurrency }} = {{ rate.toFixed(2) }} {{ currency }}
      </li>
    </ul>
  </div>
</template>

<script>
import Hero from '../Hero/Hero.vue';
import './Home.css'


export default {
  props: ['baseCurrency', 'rates'],
  components: {
    Hero
  },
  computed: {
    filteredRates() {
      const allowedCurrencies = ['RUB', 'USD', 'EUR'];
      return Object.fromEntries(
        Object.entries(this.rates).filter(([currency]) => allowedCurrencies.includes(currency))
      );
    }
  }
};
</script>


