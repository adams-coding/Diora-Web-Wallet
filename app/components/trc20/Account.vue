<template>
  <div class="account">
    <Address :address="address" @detailClick="$emit('detailClick')" />
    <div class="account-balance">
      <div class="fs15 text-right" style="color: rgba(255, 152, 0, 0.6)">Network: <b>Diora Testnet</b></div>
      <div class="account-balance-container">
        <div class="account-balance-number text-center" :style="{'font-size': `${balanceSize}px`}">
          <animated-number
          :value="balance"
          :formatValue="formatBalance"
          :duration="1000"
          />
        </div>
        <div class="account-balance-symbol text-center">{{ symbol }}</div>
      </div>
      <div class="account-balance-container">
        <div class="account-balance-number text-center" :style="{'font-size': `${defiBalanceSize}px`}">
          <animated-number
          :value="defiBalance"
          :formatValue="formatBalance"
          :duration="1000"
          />
        </div>
        <div class="account-balance-symbol text-center">DIOR</div>
      </div>
    </div>
    <div class="menu">
      <div class="menu-item" @click="$emit('transferClick')">
        <fa icon="arrow-alt-circle-right" class="fs25"/> <span class="ml30">Transfer</span>
      </div>
      <div class="menu-line"></div>
      <div class="menu-item" @click="$emit('transactionsClick')">
        <fa icon="history" class="fs25"/> <span class="ml30">Transactions</span>
      </div>
      <div class="menu-line"></div>
    </div>
  </div>
</template>

<script>
import Address from './Address';
import AnimatedNumber from "animated-number-vue";

export default {
  props: ['address', 'balance', 'symbol', 'defiBalance'],
  components: {
    Address,
    AnimatedNumber
  },
  computed: {
    balanceSize() {
      var s = this.formatBalance(this.balance);
      switch (s.length) {
        case 1: return 100;
        case 2: return 100;
        case 3: return 100;
        case 4: return 100;
        case 5: return 100;
        case 6: return 100;
        case 7: return 80;
        case 8: return 70;
        case 9: return 65;
        case 10: return 65;
      }
      return 50;
    },
    defiBalanceSize() {
      var s = this.formatBalance(this.defiBalance);
      switch (s.length) {
        case 1: return 60;
        case 2: return 60;
        case 3: return 60;
        case 4: return 60;
        case 5: return 60;
        case 6: return 60;
        case 7: return 50;
        case 8: return 40;
        case 9: return 35;
        case 10: return 35;
      }
      return 50;
    }
  },
  methods: {
    formatBalance(value) {
      if(this.balance === 0) {
        return '0';
      }
      if (this.balance < 0.01) {
        value = Math.floor(value * 10000) / 10000
        return value.toFixed(4);
      }
      value = Math.floor(value * 100) / 100
      return value.toFixed(2);
    }
  }
}
</script>


<style lang="stylus" scoped>
  .account
    background #2C2C2C
    // background-image: url(/media/bg.jpg);
    // background-size: cover;
    // background-repeat: no-repeat;
    // background-position: center;
    width 380px
    max-width 100vw
    color #ffffff
    position relative
    @media(max-width: 767px) {
      width 100vw
      height 100vh
    }
    &-balance
      padding 15px 20px

      @media(max-width 767px)
        height calc(100vh - 447px)
        position relative

      &-container
        margin-top 20px
        @media(max-width 767px)
          position absolute
          top calc(50% + 20px)
          margin-top 0
          left 0
          right 0
          transform translateY(-50%)

      &-number
        font-size 60px
        font-weight 80
        line-height 1
        transition all 0.3s

      &-symbol
        font-size 16px
        font-weight 300
        margin-bottom 10px
        opacity 0.5

    .menu
      position absolute
      bottom 0
      left 0
      right 0
      &-line
        border-top 1px solid rgba(256, 256, 256, 0.1)
      &-item
        font-size 25px
        font-weight 200
        opacity 0.7
        transition all 0.3s
        cursor pointer
        padding 0 25px
        height 70px
        display flex
        align-items center

        &:hover
          opacity 1
</style>

