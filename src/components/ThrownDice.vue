<script setup>
import { ref } from 'vue'

const dice = ref([]);

const rollDice = () => {
  dice.value = [];
  let roll;
  for (let i=1; i<6; i++) {
    roll = Math.floor(Math.random()*6) + 1;
    dice.value.push(roll);
  }
}

</script>

<template>
  <div>
    <button @click="rollDice">Gooi!</button>
  </div>

  <table>
      <tr>
        <td id="dobbelstenen" v-for="(die, index) in dice" :key="index">{{ die }}</td>
      </tr>
  </table>
</template>

<style scoped>
#dobbelstenen {
  width: 15px;
  height: 15px;
  border: 2px solid black;
  border-collapse: collapse;
  padding: 10px;
  font-size: 50x;
}
</style>
