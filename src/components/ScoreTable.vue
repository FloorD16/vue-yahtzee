<script setup>
const dice = defineModel();
</script>

<template>
    <p>{{ dice }}</p>

    <table>
        <tr>
            <td>ENEN</td>
            <td class="bovensteDeel"></td>
        </tr>
        <tr>
            <td>TWEEËN</td>
            <td class="bovensteDeel"></td>
        </tr>
        <tr>
            <td>DRIEËN</td>
            <td class="bovensteDeel"></td>
        </tr>
        <tr>
            <td>VIEREN</td>
            <td class="bovensteDeel"></td>
        </tr>
        <tr>
            <td>VIJVEN</td>
            <td class="bovensteDeel"></td>
        </tr>
        <tr>
            <td>ZESSEN</td>
            <td class="bovensteDeel"></td>
        </tr>
        <tr>
            <td>TOTAAL</td>
            <td class="totaalbovenste"></td>
        </tr>
        <tr>
            <td>BONUS</td>
            <td>35</td>
        </tr>
        <tr>
            <td>TOTAAL van de bovenste helft</td>
            <td class="totaalbovenstehelft"></td>
        </tr>
        <tr>
            <td>THREE OF A KIND</td>
            <td class="threeofakind"></td>
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
            <td class="kleinestraat"></td>
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
            <td class="chance"></td>
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
    </table>
</template>

<style scoped>

</style>