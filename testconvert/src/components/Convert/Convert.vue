<template>
  
  <h1>Конвертация валют</h1>
     <div class="converter">
    <div class="conversion-row">
      <select class="convertsection" v-model="currencyFrom" @change="convert('from')">
        <option v-for="currency in currencies" :key="currency" :value="currency">{{ currency }}</option>
      </select>
      <input class="convertinput" type="number" v-model.number="amountFrom" @input="convert('from')">
    </div>
    <div class="conversion-row">
      <select class="convertsection" v-model="currencyTo" @change="convert('from')">
        <option v-for="currency in currencies" :key="currency" :value="currency">{{ currency }}</option>
      </select>
      <input class="convertinput" type="number" v-model.number="amountTo" @input="convert('to')">
    </div>
  </div>
  </template>
  
  <script>
  import './Convert.css'
  
  export default {
    props: ['rates', 'baseCurrency'],
    data() {
      return {
        currencies: ['RUB', 'USD', 'EUR'],
        currencyFrom: this.baseCurrency,
        currencyTo: 'USD',
        amountFrom: 1,
        amountTo: 0,
      };
    },
    watch: {
      baseCurrency(newVal) {
        this.updateCurrencies(newVal);
      },
      '$route'() {
        this.updateCurrencies(this.baseCurrency);
      }
    },
    mounted() {
      this.convert('from');
    },
    methods: {
      updateCurrencies(baseCurrency) {
        this.currencyFrom = baseCurrency;
        if (this.currencyFrom === this.currencyTo) {
          this.currencyTo = this.currencies.find(currency => currency !== baseCurrency) || 'USD';
        }
        this.convert('from');
      },
      convert(direction) {
        if (direction === 'from') {
          this.amountTo = (this.amountFrom * this.rates[this.currencyTo] / this.rates[this.currencyFrom]).toFixed(2);
        } else {
          this.amountFrom = (this.amountTo * this.rates[this.currencyFrom] / this.rates[this.currencyTo]).toFixed(2);
        }
      },
    },
  };
  </script>
  
