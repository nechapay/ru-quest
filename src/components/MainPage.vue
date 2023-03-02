<script setup>
import { computed, onMounted, ref } from 'vue'
import draggable from 'vuedraggable'

const questions = [
  {
    type: 'list',
    value: {
      x: ref(''),
      y: ref('')
    },
    text: 'Итак, А.С.Пушкин. На смерть этого поэта другое «юное дарование» <b>(Х)</b> пишет стихотворение и за него ссылается на Кавказ.',
    list: [
      'Этот поэт <b>(Х)</b> на 25-летие важной исторической битвы пишет балладу <b>(Y)</b>.',
      'Этот поэт <b>(Х)</b> прожил очень мало. Он родился через 2 года после описываемого им в балладе <b>(Y)</b> сражения. Во время восстания декабристов ему было 11 лет.',
      'Даты его рождения и смерти легко запоминаются: последние две цифры зеркальны. Посчитайте, сколько же лет прожил поэт <b>(Х)</b> и отсчитайте в его балладе <b>(Y)</b> стих под таким номером.'
    ],
    correct: {
      x: 'лермонтов',
      y: 'бородино'
    },
    verb: {
      title:
        'А теперь немного из программы Русского языка: найдите в этой строке букву, использующуюся 1 раз и характеризующуюся как согласный звук, мягкий парный, глухой парный.',
      pre: '…и леса синие верхуш',
      main: 'к',
      post: 'и'
    },
    reward: 'К'
  }
]

let dragging = ref(false)
let enabled = ref(false)

const inventory = ref([
  {
    id: 0,
    value: 'К'
  },
  {
    id: 1,
    value: 'Б'
  },
  {
    id: 2,
    value: 'О'
  },
  {
    id: 3,
    value: 'Л'
  }
])

const index = ref(0)

function prevClick(evt) {
  if (index.value > 0) index.value--
}

function nextClick(evt) {
  if (index.value < questions.length - 1) index.value++
}

const isPrevVisible = computed(() => {
  return index.value > 0
})

const isNextVisible = computed(() => {
  return index.value < questions.length - 1
})

function putReward() {
  inventory[index.value].value.value = questions[index.value].reward
}
</script>
<template>
  <div class="main-page-container my-grid">
    <div class="button--left base-flex">
      <button @click="prevClick" :disabled="!isPrevVisible">назад</button>
    </div>
    <div class="question"></div>
    <div class="button--right base-flex">
      <button @click="nextClick" :disabled="!isNextVisible">вперёд</button>
    </div>
    <div class="rewards base-flex">
      <draggable
        :list="inventory"
        :disabled="!enabled"
        item-key="id"
        class="list-group"
        ghost-class="ghost"
        @start="dragging = true"
        @end="dragging = false"
      >
        <template #item="{ element }">
          <div class="list-group-item letter base-flex" :class="{ 'not-draggable': !enabled }">
            {{ element.value }}
          </div>
        </template>
      </draggable>
    </div>
  </div>
</template>

<style scoped>
.main-page-container {
  width: 90%;
  height: 90%;
  margin: 2% 5%;
  border: 1px solid black;
}

.my-grid {
  display: grid;
  grid-template-columns: 1fr 6fr 1fr;
  grid-template-rows: 3fr 1fr;
}

.button--left {
  grid-column: 1;
  grid-row: 1;
}

.question {
  grid-column: 2;
  grid-row: 1;
}

.button--right {
  grid-column: 3;
  grid-row: 1;
}

.rewards {
  grid-row: 2;
  grid-column: 1/4;
}

.base-flex {
  display: flex;
  justify-content: center;
  align-items: center;
}

.letter {
  width: 100px;
  height: 100px;
  border: 1px solid black;
  margin: 5px;
  background: linear-gradient(to bottom, #4096ee 0%, #4096ee 100%);
  user-select: none;
}

.list-group {
  display: flex;
}
</style>
