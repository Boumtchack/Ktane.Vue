<script setup>
import { ref } from 'vue'

const emit = defineEmits(['others-status'])
const CAR = ref(false)
const FRK = ref(false)
const vowel = ref(false)
const even = ref(false)
const port = ref (false)

function sendinfo(){
  emit('others-status', [CAR, FRK, vowel, even, port] )
}

</script>

<template>
  <section id="mentionsAndSerial">
    <input type="checkbox" name="car" id="car" v-model="CAR" @change="sendinfo"><label for="car">CAR</label>
    <input type="checkbox" name="frk" id="frk" v-model="FRK" @change="sendinfo"><label for="frk">FRK</label>
    <input type="checkbox" name="port" id="port" v-model="port" @change="sendinfo"><label for="port">port parallèle</label>
    <input type="checkbox" name="vowel" id="vowel" v-model="vowel" @change="sendinfo"><label for="vowel">voyelles</label>
    <input type="checkbox" name="even" id="even" v-model="even" @change="sendinfo"><label for="even">nombre pair</label>
  </section>
</template>

<style scoped>
#mentionsAndSerial {
  display: flex;
  flex-direction: column; /* Changed flex direction to top-to-bottom */
  align-items: center;
  justify-content: flex-start;
  gap: 3px;
}
input[type="checkbox"] {
  display: none;
}

label {
  border-radius: 5px;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 80px;
  width: 80px;
  color: black;
  background-color: white;
  text-align: center; /* Centers the text horizontally */
}
input[type="checkbox"]:checked + label {
  background-color: green;
}
</style>
