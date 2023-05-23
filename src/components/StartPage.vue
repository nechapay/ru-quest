<script setup>
const emits = defineEmits(['started'])
function handleStartClick() {
  emits('started')
}
</script>
<template>
  <div class="title-screen">
    <span>
      Мало кто знает, что фраза на смерть Пушкина <br /><i>«закатилось Солнце русской поэзии»</i> - это переложение слов
      Жития <br />на гибель Александра Невского: <br /><i>«Закатилось солнце земли русской»</i>. <br />
      Литература и история всегда шли рядом.<br />
      Чаще всего литература отражала страницы истории,<br />
      но иногда литература и вела историю за собой.
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
  background: rgb(135, 190, 98);
  flex-direction: column;
}

.title-screen span {
  width: 70%;
  text-align: center;
  font-size: 150%;
  background-color: white;
  text-justify: distribute;
  box-shadow: 5px 5px 5px grey;
  border-radius: 1rem;
}
</style>
