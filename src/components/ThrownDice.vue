<script setup>
import { ref } from 'vue'

const dice = ref([]);
const emit = defineEmits(['diceValues']);

const emitDice = () => {
  emit('diceValues', dice.value);
};

const rollDice = () => {
  dice.value = [];
  let roll;

  for (let i=1; i<6; i++) {
    roll = Math.floor(Math.random()*6) + 1;
    dice.value.push(roll);
  }

  emitDice();

}

</script>

<template>
  <div>
    <button @click="rollDice">Gooi!</button>
  </div>

  <table>
    <tbody>
      <tr>
        <td id="dobbelstenen" v-for="(die, index) in dice" :key="index">{{ die }}</td>
      </tr>
    </tbody>
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
