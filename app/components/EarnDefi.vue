<template>
  <div class="earndefi">
    <div v-if="isReward || isRequested">
      We sent 15 DIOR to your wallet.<br/>Each wallet can only receive once
    </div>
    <div v-else-if="error" style="color: red;">
      ERROR: {{error}}
    </div>
    <div v-else>
      <div>Hello friends, click <b>Request</b> button bellow to receive your first DIOR</div>
      <button class="btn-big btn-black mt50" @click="request">{{isRequesting ? 'requesting' : 'request'}}</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  props: ['address', 'isReward'],
  data() {
    return {
      error: '',
      isRequesting: false,
      isRequested: !!localStorage.requestedDefi || false
    }
  },
  methods: {
    request() {
      if (this.isReward || this.isRequested) return;

      this.isRequesting = true;
      this.$Progress.start()
      axios.post('api/wallets/reward/' + this.address)
      .then(({data}) => {
        this.isRequested = true;
        this.isRequesting = false;
        this.$Progress.finish()
        localStorage.requestedDefi = 'true';
      })
      .catch(ex => {
        this.error = ex.toString();
        this.$Progress.fail();
      })
    }
  }
}
</script>


<style lang="stylus" scoped>
  .earndefi
    text-align center
    margin-top 100px
    font-size 30px
    font-weight 300
    padding 30px
</style>
