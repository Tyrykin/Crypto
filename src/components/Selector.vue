<script setup>
import { ref } from "vue";

const props = defineProps({
  setCrypto: {
    type: Function,
    required: true,
  },
});

const current = ref("");

const selectItem = (val) => {
  props.setCrypto(val);
  current.value = val;
};
</script>

<template>
  <ul>
    <li @click="selectItem('BTC')" :class="current == 'BTC' ? 'active' : ''">
      Bitcoin
    </li>
    <li @click="selectItem('ETH')" :class="current == 'ETH' ? 'active' : ''">
      ETH
    </li>
    <li @click="selectItem('USDT')" :class="current == 'USDT' ? 'active' : ''">
      USDT
    </li>
  </ul>
</template>

<style scoped>
ul {
  width: 200px;
  border-radius: 3px solid black;
}

li {
  background: #24043e;

  color: white;
  padding: 20px;
}

li:hover,
li.active {
  background: #1a032d;
  cursor: pointer;
}
</style>
