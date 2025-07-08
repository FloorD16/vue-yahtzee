<script setup>
import { ref } from 'vue'

const dice = ref([]);
const emit = defineEmits(['diceValues']);

const rollDice = () => {

  dice.value = [];
 
  for (let i = 1; i < 6; i++) {
    dice.value.push(Math.floor(Math.random()*6) + 1);
  }

  emit('diceValues', dice.value);
}

</script>

<template>
  <div>
    <button @click="rollDice">Gooi!</button>
  </div>

  <table>
    <tbody>
      <tr>
        <td v-for="(die, index) in dice" :key="index">{{ die }}</td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped>
table {
  border-collapse: collapse;
  margin: 15px;
  margin-left: 50px;
}

td {
  width: 15px;
  height: 15px;
  border: 2px solid black;
  border-collapse: collapse;
  padding: 10px;
  font-size: 50x;
}
</style>
