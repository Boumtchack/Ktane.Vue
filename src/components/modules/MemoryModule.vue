<script setup>
import { ref } from 'vue'

let round = ref(1)

let result = {
  1: [],
  2: [],
  3: [],
  4: []
}
let numbers = [1, 2, 3, 4]

const states = ['Ask for displayed number', 'Ask for number position', 'Ask for position value']

let state = ref(states[0])

function checkPosition(position) {
  state.value = states[1]
}

function checkNumber(number) {
  state.value = states[2]
}

function clickDisplay(number) {
  switch (round.value) {
    case 1:
      switch (number) {
        case 1:
        case 2:
          checkPosition(2)
          'deuxieme position'
          break
        case 3:
          checkPosition(3)
          'troisieme position'
          break
        case 4:
          checkPosition(4)
          'quatrieme position'
          break
      }
      break
    case 2:
      switch (number) {
        case 1:
          'chiffre 4'
          break
        case 3:
          'première position'
          break
        case 2:
        case 4:
          'position roud 1'
          break
      }
      break
    case 3:
      switch (number) {
        case 1:
          'nombre round 2'
          break
        case 2:
          'nombre round 1'
          break
        case 3:
          'troisieme position'
          break
        case 4:
          'nombre 4'
          break
      }
      break
    case 4:
      switch (number) {
        case 1:
          'position round 1'
          break
        case 2:
          'position 1'
          break
        case 3:
        case 4:
          'position round 2'
          break
      }
      break
    case 5:
      switch (number) {
        case 1:
          'position round 1'
          break
        case 2:
          'position round 2'
          break
        case 3:
          'position round 4'
          break
        case 4:
          'position round 3'
          break
      }
      break
  }
}

function validate() {
  let displayed = document.querySelector('input[name="DisplayedNumber"]:checked')
  round.value += 1
  displayed.checked = false
  console.log(result)
}
</script>

<template>
  <div>{{ state }}</div>
  <div v-for="(number, index) in numbers" :key="index">
    <input type="radio" :id="'Display ' + number" name="DisplayedNumber" :value="number" @click="clickDisplay(number)" />
    <label :for="'Display ' + number">{{ number }}</label>
  </div>
  <div @click="validate()">validation</div>
</template>

<style scoped>
input {
  display: none;
  &:checked + label {
    background-color: red;
  }
}
</style>
