<script setup>

import { ref, computed, reactive } from 'vue'

let cost = (a) => {
  if (a < 8) {
    return -1 * (8 - a);
  } else if (a < 15) {
    return a - 8;
  } else {
    let cost = 6
    for (let i = 0; i < -1 * (14 - a); i++) {
      cost += getIncrementCost(15 + i)
    }
    return cost
  }
}

let getIncrementCost = (a) => {
  return Math.floor((a - 11) / 2)
}

const str = ref(8), dex = ref(8), con = ref(8), int = ref(8), wis = ref(8), cha = ref(8)

const totalCost = computed({
  get() {
    return cost(str.value) + cost(dex.value) + cost(con.value) + cost(int.value) + cost(wis.value) + cost(cha.value)
  }
})
</script>

<template>
  <div class="container">
    <table class="calculator">
      <thead>
        <th>Ability</th>
        <th>Score</th>
        <th>Points</th>
      </thead>
      <tbody>
        <tr>
          <td>STR:</td>
          <td><input v-model="str" type="number" id="str" name="str" min="1" value="8" /></td>
          <td>{{ cost(str) }}</td>
        </tr>
        <tr>
          <td>DEX:</td>
          <td><input v-model="dex" type="number" id="dex" name="dex" min="1" value="8" /></td>
          <td>{{ cost(dex) }}</td>
        </tr>
        <tr>
          <td>CON:</td>
          <td><input v-model="con" type="number" id="con" name="con" min="1" value="8" /></td>
          <td>{{ cost(con) }}</td>
        </tr>
        <tr :style="{ color: (int < 3) ? ('#FF0000') : ('') }">
          <td>INT:</td>
          <td><input v-model="int" type="number" id="int" name="int" min="1" value="8" /></td>
          <td>{{ cost(int) }}</td>
        </tr>
        <tr>
          <td>WIS:</td>
          <td><input v-model="wis" type="number" id="wis" name="wis" min="1" value="8" /></td>
          <td>{{ cost(wis) }}</td>
        </tr>
        <tr>
          <td>CHA:</td>
          <td><input v-model="cha" type="number" id="cha" name="cha" min="1" value="8" /></td>
          <td>{{ cost(cha) }}</td>
        </tr>
        <tr>
          <td></td>
          <td>&nbsp;&nbsp;&nbsp;&nbsp;+</td>
          <td>————</td>
        </tr>
        <tr>
          <td></td>
          <td></td>
          <td>{{ totalCost }}</td>
        </tr>
      </tbody>
    </table>
    <div>
      <p>Point buy calculator for D&D v.3.5, non-standard modifications include:</p>
      <ul>
        <li>Ability scores below 8 give a refund: 1 point per score below 8.<ul>
            <li>Characters with nonexistent ability scores (—) may not receive refunded points.</li>
          </ul>
        </li>
        <li>Ability scores can be increased above 18 with proportional point costs (19-20 +4, 21-22 +5, and so on).</li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Cabin:ital,wght@0,400..700;1,400..700&family=IM+Fell+DW+Pica:ital@0;1&family=IM+Fell+French+Canon+SC&display=swap');

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

h1 {
  font-family: 'IM Fell French Canon SC'
}

p,
li {
  font-family: 'IM Fell DW Pica';
}

table {
  font-family: 'Cabin';
}

input {
  width: 5ch
}

.calculator, input {
  font-size: xx-large;
}

td {
  text-align: right;
}

</style>
