<template>
  <ul>
    <li
      @click="setCrypto('BTC')"
      :className="cryptoNow === 'BTC' ? 'active' : ''"
    >
      Bitcoin
    </li>
    <li
      @click="setCrypto('ETH')"
      :className="cryptoNow === 'ETH' ? 'active' : ''"
    >
      ETH
    </li>
    <li
      @click="setCrypto('USDT')"
      :className="cryptoNow === 'USDT' ? 'active' : ''"
    >
      USDT
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    setCrypto: {
      type: Function,
      required: true,
    },
    cryptoNow: {
      type: String,
      required: true,
    },
 
  },
};
</script>

<style scoped>
ul {
  width: 200px;
  list-style-type: none;
  border-radius: 3px;
  border: 3px solid #000;
  padding: 0;
}
li {
  display: block;
  background: #1a032d;
  color: #fff;
  padding: 20px 0;
}
li:hover,
li.active {
  background: #0e0118;
  cursor: pointer;
}
</style>
