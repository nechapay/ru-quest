<script setup>
import Copyright from './components/Copyright.vue'
import StartPage from './components/StartPage.vue'
import EndPage from './components/EndPage.vue'
import MainPage from './components/MainPage.vue'
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
    <main-page v-if="started && !ended" />
  </transition>
  <transition name="fade-start">
    <end-page v-if="ended" />
  </transition>
  <Copyright />
</template>

<style scoped></style>
