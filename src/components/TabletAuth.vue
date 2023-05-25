<script setup>
import { ref } from 'vue'

const props = defineProps(['password'])
let output = ref('')
let showErrorMessage = ref(false)

let emits = defineEmits(['passed'])

function handleDigitClick(evt) {
  if (output.value.length < 4) {
    output.value += evt.target.value
  }
  if (showErrorMessage.value && output.value.length === 4) {
    showErrorMessage.value = false
    output.value = '' + evt.target.value
  }
  if (output.value === props.password.correct) {
    setTimeout(() => {
      emits('passed')
    }, 500)
  } else {
    if (output.value.length === 4) showErrorMessage.value = true
  }
}
</script>
<template>
  <div class="auth-container fill base-flex flex-column">
    <div class="auth-info base-flex flex-column">
      <div>Для разблокировки доступа введите пароль.</div>
      <Transition name="fade">
        <span class="auth-error-message" v-if="showErrorMessage">Пароль не подходит, попробуйте ещё раз.</span>
      </Transition>

      <span class="auth-output">{{ output }}</span>
    </div>
    <div class="auth-controls">
      <button class="digit-button" value="1" @click="handleDigitClick">1</button>
      <button class="digit-button" value="2" @click="handleDigitClick">2</button>
      <button class="digit-button" value="3" @click="handleDigitClick">3</button>
      <button class="digit-button" value="4" @click="handleDigitClick">4</button>
      <button class="digit-button" value="5" @click="handleDigitClick">5</button>
      <button class="digit-button" value="6" @click="handleDigitClick">6</button>
      <button class="digit-button" value="7" @click="handleDigitClick">7</button>
      <button class="digit-button" value="8" @click="handleDigitClick">8</button>
      <button class="digit-button" value="9" @click="handleDigitClick">9</button>
      <div class="blank-space"></div>
      <button class="digit-button" value="0" @click="handleDigitClick">0</button>
      <div class="blank-space"></div>
    </div>
  </div>
</template>

<style lang="css" scoped>
.auth-container {
  padding: 1%;
}

.auth-info {
  width: 100%;
  height: 50%;
}

.auth-controls {
  display: grid;
  width: 100%;
  height: 50%;
  gap: 1px;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr 1fr;
}

.digit-button {
  font-size: 2rem;
  background: white;
  border: 1px solid green;
  transition-duration: 0.3s;
}

.digit-button:hover {
  background: green;
  color: white;
}

.auth-output {
  margin-top: auto;
  margin-bottom: 2%;
  font-weight: bolder;
}

.auth-error-message {
  color: rgb(247, 89, 89);
  margin-top: 10%;
}
</style>
