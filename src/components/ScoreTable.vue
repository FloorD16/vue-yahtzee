<script setup>
import { ref, watch, computed } from 'vue';

const dice = defineModel();
const upperPart = ref([]);

watch(dice, (newDice) => {
    upperPart.value = [{key:1, name:'ENEN', frequency:0}, 
        {key:2, name:'TWEEËN', frequency:0}, 
        {key:3, name:'DRIEËN', frequency:0}, 
        {key:4, name:'VIEREN', frequency:0}, 
        {key:5, name:'VIJVEN', frequency:0}, 
        {key:6, name:'ZESSEN', frequency:0}];
    
    for (let die of newDice) {
        upperPart.value[die-1].frequency++;
    }

}, {immediate: true});

const totalUpperPartNoBonus = computed(() => {
    return upperPart.value.reduce((sum, item) => sum + item.key*item.frequency, 0);
});

const bonus = computed(() => {
    return totalUpperPartNoBonus.value >= 63 ? 35 : '--';
});

const totalUpperPart = computed(() => {
    return bonus.value === 35 ? totalUpperPartNoBonus.value + bonus.value : totalUpperPartNoBonus.value;
});

const sumOfAll = computed(() => {
    return dice.value.reduce((sum, die) => sum + die, 0);
});

const checkForSameDice = (count) => {
    return upperPart.value.some(item => item.frequency >= count) ? sumOfAll.value : 0;
};

const checkThreeOfKind = computed(() => checkForSameDice(3));
const checkFourOfKind = computed(() => checkForSameDice(4));
const checkFiveOfKind = computed(() => checkForSameDice(5));

const fullHouse = computed(() => {
    let frequencyEqualToTwo = false;
    let frequencyEqualToThree = false;
    for (let item of upperPart.value) {
        if (item.frequency === 2) {
            frequencyEqualToTwo = true;
        }
        if (item.frequency === 3) {
            frequencyEqualToThree = true;
        }
    }
    return frequencyEqualToTwo && frequencyEqualToThree ? 25 : 0;
});

const sortDice = computed(() => {
    return [...new Set(dice.value)].sort((a,b) => a-b).join(',');
});

const smallStreet = computed(() => {
    if (sortDice.value.includes('1,2,3,4') || 
    sortDice.value.includes('2,3,4,5') ||
    sortDice.value.includes('3,4,5,6')) {
        return 30;
    } else {
        return 0;
    }
});

const bigStreet = computed(() => {
    if (sortDice.value.includes('1,2,3,4,5') || 
    sortDice.value.includes('2,3,4,5,6')) {
        return 40;
    } else {
        return 0;
    }
});

const totalLowerPart = computed(() => {
    return checkThreeOfKind.value + checkFourOfKind.value + fullHouse.value + smallStreet.value + bigStreet.value + checkFiveOfKind.value + sumOfAll.value;
})

const totalScore = computed(() => {
    return totalUpperPart.value + totalLowerPart.value;
});
</script>

<template>
    <table>
        <tbody>
            <tr v-for="item in upperPart" :key="item.key">
                <td>{{ item.name }}</td>
                <td>{{ item.key * item.frequency }}</td>
            </tr>
            <tr>
                <td>TOTAAL</td>
                <td>{{ totalUpperPartNoBonus }}</td>
            </tr>
            <tr>
                <td>BONUS</td>
                <td>{{ bonus }}</td>
            </tr>
            <tr>
                <td>TOTAAL van de bovenste helft</td>
                <td>{{ totalUpperPart }}</td>
            </tr>
            <tr>
                <td>THREE OF A KIND</td>
                <td>{{ checkThreeOfKind }}</td>
            </tr>
            <tr>
                <td>CARRÉ</td>
                <td>{{ checkFourOfKind }}</td>
            </tr>
            <tr>
                <td>FULL HOUSE</td>
                <td>{{ fullHouse }}</td>
            </tr>
            <tr>
                <td>KLEINE STRAAT</td>
                <td>{{ smallStreet }}</td>
            </tr>
            <tr>
                <td>GROTE STRAAT</td>
                <td>{{ bigStreet }}</td>
            </tr>
            <tr>
                <td>YAHTZEE</td>
                <td>{{ checkFiveOfKind }}</td>
            </tr>
            <tr>
                <td>CHANCE</td>
                <td>{{ sumOfAll }}</td>
            </tr>
            <tr>
                <td>TOTAAL van de onderste helft</td>
                <td>{{ totalLowerPart }}</td>
            </tr>
            <tr>
                <td>TOTAAL van de bovenste helft</td>
                <td>{{ totalUpperPart }}</td>
            </tr>
            <tr>
                <td>TOTAAL</td>
                <td>{{ totalScore }}</td>
            </tr>
        </tbody>
    </table>
</template>

<style scoped>
    table {
        border-collapse: collapse;
    }
    
    td {
        border: 1px solid black;
        padding: 5px 15px;
    }
</style>