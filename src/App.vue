<script setup>
import { ref } from 'vue';
import ThrownDice from './components/ThrownDice.vue';
import ScoreTable from './components/ScoreTable.vue';

const dice = ref([]);

const setDice = (newDice) => {
    dice.value = newDice;
}
</script>

<template>
    <ThrownDice @diceValues="setDice"/>
    <ScoreTable v-model="dice"/>
</template>

<style scoped></style>
