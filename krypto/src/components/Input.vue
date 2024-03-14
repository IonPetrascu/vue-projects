<template>
  <input
    type="number"
    min="0"
    @input="changeAmount($event.target.value)"
    placeholder="Введите число"
  />
  <button @click="convert()">Конвертировать</button>
  <button @click="favourite()">В избранное</button>
</template>

<script>
export default {
  props: {
    changeAmount: {
      type: Function,
      required: true,
    },
    convert: {
      type: Function,
      required: true,
    },
    favourite: {
      type: Function,
      required: true,
    },
  },
};
</script>

<style scoped>
input {
  border-radius: 3px;
  border: 0;
  padding: 10px 15px;
  background-color: azure;
  color: #333;
  outline: none;
  width: 500px;
  top: -50px;
  font-size: 1.2em;
}
button {
  padding: 10px 10px;
  display: block;
  margin: 0 auto;
  margin-top: 40px;
  margin-bottom: 20px;
  color: #fff;
  text-transform: uppercase;
  cursor: pointer;
  background-color: #4c20eb;
  border: none;
  border-radius: 3px;
}
</style>
