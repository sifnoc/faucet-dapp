<template>
  <div id="app">
    <faucet-header></faucet-header>
    <faucet-body>
      <div slot="faucet">
        <input type="text"
          v-model="accountToFaucetPeth"
        >
        <button
          v-on:click="faucetPeth"
        > faucet </button>
      </div>
    </faucet-body>
    <faucet-body>
      <div slot="faucet">
        <input type="text"
          v-model="accountToFaucetToken"
        >
        <button
          v-on:click="faucetToken"
        > faucet </button>
      </div>
    </faucet-body>
    <faucet-footer
      v-bind:transactions="transactions"
    ></faucet-footer>
  </div>
</template>

<script>
import FaucetHeader from './components/FaucetHeader.vue';
import FaucetBody from './components/FaucetBody.vue';
import FaucetFooter from './components/FaucetFooter.vue';
import Web3 from 'web3';

export default {
  name: 'app',
  data() {
    return {
      web3: null,
      operator: null,
      accountToFaucetPeth: null,
      accountToFaucetToken: null,
      transactions: []
    }
  },
  components: {
    'faucet-header': FaucetHeader,
    'faucet-body': FaucetBody,
    'faucet-footer': FaucetFooter
  },
  created () {
    const that = this;
    this.web3 = new Web3('http://localhost:8545');
    this.web3.eth.getAccounts((err, accounts) => {
      if (!err) {
        that.operator = accounts[0]
      }
    });
  },
  methods: {
    faucetPeth: async function () {
      console.log(this.accountToFaucetPeth);
      if (!this.web3.utils.isAddress(this.accountToFaucetPeth)) {
        alert('invalid address');
        return;
      }
      this.web3.eth.sendTransaction({from: this.operator, to: this.accountToFaucetPeth, value: 1000000000000000000, gasPrice: 1}, (err, hash) => {
        if (!err) {
          this.transactions.push(hash);
        }
      })
    },
    faucetToken: async function () {
      if (!this.web3.utils.isAddress(this.accountToFaucetToken)) {
        alert('invalid address');
        return;
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
