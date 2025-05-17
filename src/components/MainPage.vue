<script setup>
import { ref } from 'vue'
import BatteriesSetup from './setup/BatteriesSetup.vue'
import ErrorsNumber from './setup/ErrorsNumber.vue'
import MentionsAndSerial from './setup/MentionsAndSerial.vue'
import ButtonsModule from './modules/ButtonsModule.vue';
import SimpleWireModule from './modules/SimpleWireModule.vue';
import ComplexWireModule from './modules/ComplexWireModule.vue';
import SimonSays from './modules/SimonSays.vue';
import KeyPads from './modules/KeyPads.vue';
import WhosFirst from './modules/WhosFirst.vue';
import MemoryModule from './modules/MemoryModule.vue';

const titles = ['Buttons', 'Simple wires', 'Complex wires', 'Simon says', 'Keypads', "Who's First", 'Memory', 'Morse Code', 'Maze', 'Password', 'Needy']

let batteriesAmount = ref(0)
function updateBatteriesAmount(value) {
  batteriesAmount.value = value
}
let errorAmount = ref(0)
function updateErrorAmount(value) {
  errorAmount.value = value
}

let CAR = ref(false)
let FRK = ref(false)
let vowel = ref(false)
let serialEven = ref(false)
let port = ref(false)

function updateOthers(array) {
  CAR.value = array[0].value
  FRK.value = array[1].value
  vowel.value = array[2].value
  serialEven.value = array[3].value
  port.value = array[4].value
}

const isSetupOpen = ref(true);
function toggleSetup() {
  isSetupOpen.value = !isSetupOpen.value;
}

const moduleComponents = [
  ButtonsModule,
  SimpleWireModule,
  ComplexWireModule, 
  SimonSays,
  KeyPads,
  WhosFirst,
  MemoryModule,
  null, // Placeholder for Morse Code
  null, // Placeholder for Maze
  null, // Placeholder for Password
];

const openModals = ref(Array(titles.length).fill(false));
function toggleModal(index) {
  openModals.value[index] = !openModals.value[index];
}
</script>

<template>
  <div>
    <div class="settings-button" :class="{ 'open': isSetupOpen }" @click="toggleSetup"></div>
    <div v-if="isSetupOpen" class="modal-overlay" @click="toggleSetup"></div>
    <div class="setup-container" :class="{ 'closed': !isSetupOpen }">
      <section class="setups">
        <ErrorsNumber @amount-of-error="updateErrorAmount" />
        <MentionsAndSerial @others-status="updateOthers" />
        <BatteriesSetup @amount-of-batteries="updateBatteriesAmount" />
      </section>
    </div>
  </div>
  <section class="modules">
    <div v-for="(title, index) in titles" :key="index">
      <div class="module-title" @click="toggleModal(index)">{{ title }}</div>
      <div v-if="openModals[index]" class="module-modal">
        <component :is="moduleComponents[index]" v-if="moduleComponents[index]" />
        <p v-else>Module not implemented yet.</p>
      </div>
    </div>
  </section>
</template>

<style>
.settings-button {
  position: fixed;
  top: 10px;
  right: 10px;
  width: 30px; 
  height: 30px; 
  margin: 10  px; 
  background-image: url('/settings-svgrepo-com.svg');
  background-size: cover;
  background-position: center;
  cursor: pointer;
  z-index: 1100; 
  transition: background-image 0.3s ease;
}

.settings-button.open {
  background-image: url('/cross.svg.png'); /* Change to cross image when open */
}

.setup-container {
  display: flex;
  flex-direction: row; /* Ensures setups are ordered left to right */
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 10px; /* Position near the top */
  right: 10px; /* Align to the right */
  background-color: white; /* Modal background */
  border: 1px solid #ccc;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
  z-index: 1000; /* Ensure it appears above other elements */
  transition: opacity 0.3s ease, visibility 0.3s ease;
  opacity: 1;
  visibility: visible;
}

.setup-container.closed {
  opacity: 0;
  visibility: hidden;
}

.setups {
  display: flex;
  flex-direction: row; /* Ensures setups are ordered left to right */
  gap: 20px;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5); /* Dimmed background */
  z-index: 999; /* Below the modal but above other content */
  opacity: 1;
  visibility: visible;
  transition: opacity 0.3s ease, visibility 0.3s ease;
}

.modal-overlay.hidden {
  opacity: 0;
  visibility: hidden;
}

.modules {
  text-align: center;
}

.module-title {
  cursor: pointer;
  font-weight: bold;
  margin: 10px 0;
}

.module-modal {
  background-color: white;
  border: 1px solid #ccc;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  padding: 10px;
  margin-top: 5px;
}
</style>