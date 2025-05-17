<script setup>
import { ref } from 'vue'

const emit = defineEmits(['amount-of-error'])
const errorAmount = ref(0)

function sendError(){
  emit('amount-of-error', errorAmount.value)
}

</script>

<template>
  <section id="error">
    <input type="radio" id="zero" :value="0" v-model="errorAmount" @change="sendError" checked />
    <label for="zero">0</label>
    <input type="radio" id="one" :value="1" v-model="errorAmount" @change="sendError" />
    <label for="one">1</label>
    <input type="radio" id="two" :value="2" v-model="errorAmount" @change="sendError" />
    <label for="two">2</label>
  </section>
</template>

<style scoped>
#error {
  display: flex;
  flex-direction: column; /* Changed flex direction to top-to-bottom */
  align-items: center;
  gap: 3px;
}
input[type="radio"] {
  display: none;
}
label {
  border-radius: 5px;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100px;
  width: 100px;
  color: black;
  font-size: 20px;
  font-weight: bold;
  background-image: url('/hexagon.svg'); /* Set the alert-error SVG as the background */
  background-size: cover; /* Ensures the image stretches to fill the label */
  background-position: center; /* Centers the image */
  text-align: center; /* Centers the text horizontally */
}

input[type="radio"]:checked + label {
  background-color: red;
}

</style>
