<script setup>
import TheCanvas from './components/TheCanvas.vue'
import Copyright from './components/Copyright.vue'
import StartPage from './components/StartPage.vue'
import EndPage from './components/EndPage.vue'
import { computed, watch, ref } from 'vue'

let started = ref(false)
let ended = ref(false)

function handleStarted() {
  started.value = true
}
</script>

<template>
  <transition name="fade-start">
    <start-page v-if="!started && !ended" @started="handleStarted" />
  </transition>
  <transition name="fade-start">
    <end-page v-if="ended" />
  </transition>
  <Copyright />
</template>

<style scoped></style>
