<script setup>
import { computed, onMounted, ref } from 'vue'
import draggable from 'vuedraggable'
import Table from '../components/Table.vue'
import TableDialog from '../components/TableDialog.vue'

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
      pre: '…',
      main: 'и леса синие верхушки',
      post: '.',
      reward: 'К',
      correct: 'к'
    }
  }
]

let dragging = ref(false)
let enabled = ref(true)

const inventory = ref([
  {
    id: 0,
    value: ''
  },
  {
    id: 1,
    value: ''
  },
  {
    id: 2,
    value: ''
  },
  {
    id: 3,
    value: ''
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
    <div class="question">
      <div class="table-container"><Table /></div>
      <div class="table-container"><Table /></div>
      <div class="table-container"><Table /></div>
      <div class="table-container"><Table /></div>
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
  grid-template-columns: 1fr;
  grid-template-rows: 3fr 1fr;
}
.question {
  grid-column: 1;
  grid-row: 1;
  display: flex;
  flex-wrap: wrap;
}

.table-container {
  width: 40%;
  margin-top: 2.5%;
  margin-left: 7%;
}
.rewards {
  grid-row: 2;
  grid-column: 1;
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
