<script setup>
import { computed, defineEmits, onMounted, ref, watch } from 'vue'
const emits = defineEmits(['started'])
function handleStartClick() {
  emits('started')
}
</script>
<template>
  <div class="title-screen">
    <span>
      Мало кто знает, что фраза на смерть Пушкина <br /><i>«закатилось Солнце русской поэзии»</i> - это переложение слов
      Жития на гибель Александра Невского: <br /><i>«Закатилось солнце земли русской»</i>. <br />
      Литература и история всегда шли рядом. Чаще всего литература отражала страницы истории, но иногда литература и
      вела историю за собой.
    </span>
    <button @click="handleStartClick" class="button-5">Начать</button>
  </div>
</template>

<style scoped>
.title-screen {
  display: flex;
  width: 100%;
  height: 100%;
  align-items: center;
  justify-content: center;
  background: grey;
  flex-direction: column;
}

.title-screen span {
  width: 70%;
  text-align: center;
  font-size: 200%;
}
.button-5 {
  align-items: center;
  background-clip: padding-box;
  background-color: #fa6400;
  border: 1px solid transparent;
  border-radius: 0.25rem;
  box-shadow: rgba(0, 0, 0, 0.02) 0 1px 3px 0;
  box-sizing: border-box;
  color: #fff;
  cursor: pointer;
  display: inline-flex;
  font-family: system-ui, -apple-system, system-ui, 'Helvetica Neue', Helvetica, Arial, sans-serif;
  font-size: 16px;
  font-weight: 600;
  justify-content: center;
  line-height: 1.25;
  margin: 0;
  min-height: 3rem;
  padding: calc(0.875rem - 1px) calc(1.5rem - 1px);
  position: relative;
  text-decoration: none;
  transition: all 250ms;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  vertical-align: baseline;
  width: auto;
}

.button-5:hover,
.button-5:focus {
  background-color: #fb8332;
  box-shadow: rgba(0, 0, 0, 0.1) 0 4px 12px;
}

.button-5:hover {
  transform: translateY(-1px);
}

.button-5:active {
  background-color: #c85000;
  box-shadow: rgba(0, 0, 0, 0.06) 0 2px 4px;
  transform: translateY(0);
}
</style>
