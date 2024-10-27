<script setup>
import CryptoConvert from "crypto-convert";
import Input from "./components/Input.vue";
import Selector from "./components/Selector.vue";
import { ref } from "vue";
const convert = new CryptoConvert();
const amount = ref(0);
const cryptoFirst = ref("");
const cryptoSecond = ref("");
const error = ref("");
const result = ref(0);

const changeAmount = (val) => {
  amount.value = val;
};
const setCryptoFirst = (val) => {
  cryptoFirst.value = val;
};
const setCryptoSecond = (val) => {
  cryptoSecond.value = val;
};

const convertCrypto = async () => {
  if (amount.value <= 0) {
    error.value = "Введите число больше 0";
    return;
  } else if (cryptoFirst.value == "" || cryptoSecond.value == "") {
    error.value = "Выберите криптовалюту";
    return;
  } else if (cryptoFirst.value == cryptoSecond.value) {
    error.value = "Выберите другую криптовалюту";
    return;
  } else {
    error.value = "";
    await convert.ready();
    if (cryptoFirst.value == "BTC" && cryptoSecond.value == "USDT")
      result.value = convert.BTC.USDT(amount.value);
    else if (cryptoFirst.value == "BTC" && cryptoSecond.value == "ETH")
      result.value = convert.BTC.ETH(amount.value);
    else if (cryptoFirst.value == "USDT" && cryptoSecond.value == "BTC")
      result.value = convert.USDT.BTC(amount.value);
    else if (cryptoFirst.value == "USDT" && cryptoSecond.value == "ETH")
      result.value = convert.USDT.ETH(amount.value);
    else if (cryptoFirst.value == "ETH" && cryptoSecond.value == "BTC")
      result.value = convert.ETH.BTC(amount.value);
    else if (cryptoFirst.value == "ETH" && cryptoSecond.value == "USDT")
      result.value = convert.ETH.USDT(amount.value);
  }
};
</script>

<template>
  <div class="container">
    <Input :changeAmount="changeAmount" :convertCrypto="convertCrypto" />
    <div class="wrapper__result">
    	<p v-if="error != ''">{{ error }}</p>
	    <p v-if="result != 0" class="result-text">{{ result }}</p>
    </div>
    <div class="wrapper__selector">
      <Selector :setCrypto="setCryptoFirst" />
      <Selector :setCrypto="setCryptoSecond" />
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

.wrapper__result {
	height: 100px;
	
	
}

.wrapper__selector {
  display: flex;
  gap: 100px;
}
</style>
