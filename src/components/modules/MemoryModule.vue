<script setup>
import { ref } from 'vue'

let round = ref(1)

let result = {
  1: [],
  2: [],
  3: [],
  4: [],
  5: []
}
let numbers = [1, 2, 3, 4]

const states = ['Ask for displayed number', 'Ask for position of number ', 'Ask for value of position ']

let state = ref(states[0])

function checkPosition(position) {
  if (round.value < 5) {
    result[round.value][1] = position
    state.value = states[2] + position
  } else {
    state.value = 'finished, reset the module'
  }
}

function checkNumber(number) {
  state.value = states[1] + number
  result[round.value][0] = number
}

function pickPosition(position) {
  result[round.value][1] = position
  state.value = states[0]
  round.value += 1
}

function pickNumber(number) {
  result[round.value][0] = number
  state.value = states[0]
  round.value += 1
}

function manageTurn(number) {
  console.log(result)
  if (state.value == states[0]) {
    pickDisplay(number)
  } else if (state.value.slice(0, -1) == states[1]) {
    pickPosition(number)
  } else if (state.value.slice(0, -1) == states[2]) {
    pickNumber(number)
  }
}

function pickDisplay(number) {
  switch (round.value) {
    case 1:
      switch (number) {
        case 1:
        case 2:
          checkPosition(2)
          break
        case 3:
          checkPosition(3)
          break
        case 4:
          checkPosition(4)
          break
      }
      break
    case 2:
      switch (number) {
        case 1:
          checkNumber(4)
          break
        case 3:
          checkPosition(1)
          break
        case 2:
        case 4:
          'position roud 1'
          checkPosition(result[1][1])
          break
      }
      break
    case 3:
      switch (number) {
        case 1:
          'number round 2'
          checkNumber(result[2][0])
          break
        case 2:
          'number round 1'
          checkNumber(result[1][0])
          break
        case 3:
          checkPosition(3)
          break
        case 4:
          checkNumber(4)
          break
      }
      break
    case 4:
      switch (number) {
        case 1:
          'position round 1'
          checkNumber(result[1][1])
          break
        case 2:
          checkPosition(1)
          break
        case 3:
        case 4:
          'position round 2'
          checkPosition(result[2][1])
          break
      }
      break
    case 5:
      switch (number) {
        case 1:
          state.value = `click on ${result[1][0]} then reset the module`
          break
        case 2:
          state.value = `click on ${result[2][0]} then reset the module`
          break
        case 3:
          state.value = `click on ${result[4][0]} then reset the module`
          break
        case 4:
          state.value = `click on ${result[3][0]} then reset the module`
          break
      }
      break
  }
}

function reset() {
  result = {
    1: [],
    2: [],
    3: [],
    4: [],
    5: []
  }
  round.value = 1
  state.value = states[0]
}
</script>

<template>
  <div>{{ state }}</div>
  <div v-for="(number, index) in numbers" :key="index">
    <input type="radio" :id="'Display ' + number" name="DisplayedNumber" :value="number" @click="manageTurn(number)" />
    <label :for="'Display ' + number">{{ number }}</label>
  </div>

  <div @click="reset()">reset</div>
</template>

<style scoped>
input {
  display: none;
  &:hover + label {
    background-color: green;
  }
}
</style>
