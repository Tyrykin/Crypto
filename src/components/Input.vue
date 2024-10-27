<script setup>
import { ref } from "vue";
const props = defineProps({
  changeAmount: {
    type: Function,
    required: true,
  },
  convertCrypto: {
    type: Function,
    required: true,
  },
});
</script>

<template>
  <div class="container">
    <h1>Crypto</h1>
    <input
      type="number"
      @input="changeAmount($event.target.value)"
      placeholder="Введите число"
      min="0"
      oninput="validity.valid||(value='')"
    />
    <button @click="props.convertCrypto">Конвертировать</button>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

input {
  border-radius: 3px;
  padding: 10px 15px;
  background-color: rgb(255, 255, 255);
  color: black;
  width: 500px;
}

button {
  border-radius: 3px;
  padding: 15px 20px;
  background-color: #24043e;
  color: white;
  cursor: pointer;
}

button:hover {
  background-color: #1a032d;
}
</style>
