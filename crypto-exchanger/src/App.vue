<template>
  <TopHeader @walletConnection="saveWalletPublicKey"></TopHeader>
  <ExchangerBody :walletPublicKey="walletPublicKey"></ExchangerBody>
</template>

<script>
import TopHeader from './components/TopHeader.vue';
import ExchangerBody from './components/ExchangerBody.vue';

export default {
  name: 'App',
  components: {
    TopHeader,
    ExchangerBody,
  },
  data(){
    return{
      walletPublicKey: null,
    }
  },
  methods: {
    saveWalletPublicKey(value){
      this.walletPublicKey = value.walletPublicKey;
    },
  },
}
</script>

<style>
body{
  background-color: #090909;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
