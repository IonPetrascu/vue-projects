<template>
  <h1>CRYPTO</h1>
  <Input
    :convert="convert"
    :changeAmount="changeAmount"
    :favourite="favourite"
  />
  <p v-if="error !== ''">{{ error }}</p>
  <p className="result" v-if="result !== 0">{{ result }}</p>
  <Favourite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs" />
  <div className="selectors">
    <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst" />
    <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond" />
  </div>
</template>

<script>
import Input from "./components/Input.vue";
import Selector from "./components/Selector.vue";
import CryptoConvert from "crypto-convert";
import Favourite from "./components/Favourite.vue";

const convert = new CryptoConvert();

export default {
  components: {
    Input,
    Selector,
    Favourite,
  },
  data() {
    return {
      amount: 0,
      cryptoFirst: "",
      cryptoSecond: "",
      error: "",
      result: 0,
      favs: [],
    };
  },
  methods: {
    changeAmount(val) {
      this.amount = val;
    },
    setCryptoFirst(val) {
      this.cryptoFirst = val;
    },
    setCryptoSecond(val) {
      this.cryptoSecond = val;
    },
    async convert() {
      if (this.amount <= 0) {
        this.error = "Введите число больше за ноль";
        return;
      } else if (this.cryptoFirst === "" || this.cryptoSecond === "") {
        this.error = "Выберите вылюту";
        return;
      } else if (this.cryptoFirst === this.cryptoSecond) {
        this.error = "Выберите другую валюту";
        return;
      }

      this.error = "";
      await convert.ready();
      if (this.cryptoFirst === "BTC" && this.cryptoSecond === "ETH") {
        this.result = convert.BTC.ETH(this.amount);
      } else if (this.cryptoFirst === "BTC" && this.cryptoSecond === "USDT") {
        this.result = convert.BTC.USDT(this.amount);
      } else if (this.cryptoFirst === "ETH" && this.cryptoSecond === "USDT") {
        this.result = convert.ETH.USDT(this.amount);
      } else if (this.cryptoFirst === "ETH" && this.cryptoSecond === "BTC") {
        this.result = convert.ETH.BTC(this.amount);
      } else if (this.cryptoFirst === "USDT" && this.cryptoSecond === "USDT") {
        this.result = convert.USDT.USDT(this.amount);
      } else if (this.cryptoFirst === "USDT" && this.cryptoSecond === "BTC") {
        this.result = convert.USDT.BTC(this.amount);
      }
    },
    favourite() {
      this.favs.push({
        from: this.cryptoFirst,
        to: this.cryptoSecond,
      });
    },
    getFromFavs(index) {
      this.cryptoFirst = this.favs[index].from;
      this.cryptoSecond = this.favs[index].to;
    },
  },
};
</script>

<style scoped>
.selectors {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 700px;
  margin: 0 auto;
}
.result {
  background-color: white;
  width: min-content;
  margin: 0 auto;
  border-radius: 10px;
  padding: 20px;
  text-align: center;
}
</style>
