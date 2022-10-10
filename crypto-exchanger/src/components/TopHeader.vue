<template>
  <div class="header py-3">
    <div class="container">
      <div class="row text-end justify-content-end">
      <button v-if="walletPublicKey === null" class="wallet col-2 py-1" @click="connectWallet">Connect wallet</button>
      <div v-if="walletPublicKey !== null" class="wallet col-2 py-1 text-center">
        <p class="my-auto">{{walletPublicKey.substr(0,4)}}...{{walletPublicKey.substr(walletPublicKey.length - 4, 4)}}</p>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TopHeader',
  data(){
    return{
      walletPublicKey: null,
      ethereum: undefined,
    }
  },
  methods:{
    async connectWallet(){
      const ethereum = this.ethereum;
      try{
        this.walletPublicKey = await ethereum.request({method: 'eth_requestAccounts'});
        this.$emit('walletConnection', {walletPublicKey: this.walletPublicKey});
      }
      catch(error){
        if (ethereum === undefined){
          console.log('You do not have metamask!');
        } 
        else{
          console.log(error);
        }
      }
    },
  },
  created:
    function(){
      this.ethereum = window.ethereum;
      if (typeof this.ethereum !== 'undefined') {
        console.log('MetaMask is installed!');
      }
      else{
        console.log('You must install metamask before using this app')
      }
    }
}
</script>

<style scoped>
  .header{
    background-color: #060538;
  }
  .wallet{
    border: 0px;
    border-radius: 16px;
    outline: none;
    background-color: #090909;
    color: #7B7B7B;
  }
  .wallet:hover{

  }
</style>
