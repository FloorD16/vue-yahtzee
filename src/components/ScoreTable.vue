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

const checkForSameDice = computed(() => {
    for (let item of upperPart.value) {
        if (item.frequency >= 3) {
            return sumOfAll.value;
        }
    }
    return 0;
});

const sortString = computed(() => {
    return [...new Set(dice.value)].sort((a,b) => a-b).join(',');
});

const smallStreet = computed(() => {
    if (sortString.value.includes('1,2,3,4') || 
    sortString.value.includes('2,3,4,5') ||
    sortString.value.includes('3,4,5,6')) {
        return 30;
    } else {
        return 0;
    }
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
                <td>{{ checkForSameDice }}</td>
            </tr>
            <tr>
                <td>CARRÉ</td>
                <td class="carré"></td>
            </tr>
            <tr>
                <td>FULL HOUSE</td>
                <td class="fullhouse"></td>
            </tr>
            <tr>
                <td>KLEINE STRAAT</td>
                <td>{{ smallStreet }}</td>
            </tr>
            <tr>
                <td>GROTE STRAAT</td>
                <td class="grotestraat"></td>
            </tr>
            <tr>
                <td>YAHTZEE</td>
                <td class="yahtzee"></td>
            </tr>
            <tr>
                <td>CHANCE</td>
                <td>{{ sumOfAll }}</td>
            </tr>
            <tr>
                <td>TOTAAL van de onderste helft</td>
                <td class="totaalonderstehelft"></td>
            </tr>
            <tr>
                <td>TOTAAL van de bovenste helft</td>
                <td class="totaalbovenstehelft"></td>
            </tr>
            <tr>
                <td>TOTAAL</td>
                <td class="totaal"></td>
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