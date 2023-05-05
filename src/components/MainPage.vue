<script setup>
import { computed, onMounted, ref } from 'vue'
import draggable from 'vuedraggable'
import Table from './Table.vue'
import TableDialog from './TableDialog.vue'
import Inventory from './Inventory.vue'

const questions = [
  {
    type: 'list',
    text: 'Итак, А.С.Пушкин. На смерть этого поэта другое «юное дарование» <b>(Х)</b> пишет стихотворение и за него ссылается на Кавказ.',
    list: [
      'Этот поэт <b>(Х)</b> на 25-летие важной исторической битвы пишет балладу <b>(Y)</b>.',
      'Этот поэт <b>(Х)</b> прожил очень мало. Он родился через 2 года после описываемого им в балладе <b>(Y)</b> сражения. Во время восстания декабристов ему было 11 лет.',
      'Даты его рождения и смерти легко запоминаются: последние две цифры зеркальны. Посчитайте, сколько же лет прожил поэт <b>(Х)</b> и отсчитайте в его балладе <b>(Y)</b> стих под таким номером.'
    ],
    verb: {
      text: [
        {
          id: 1,
          line: '— Скажи-ка, дядя, ведь недаром',
          correct: false,
          blank: false
        },
        {
          id: 2,
          line: 'Москва, спаленная пожаром,',
          correct: false,
          blank: false
        },
        {
          id: 3,
          line: 'Французу отдана?',
          correct: false,
          blank: false
        },
        {
          id: 4,
          line: 'Ведь были ж схватки боевые,',
          correct: false,
          blank: false
        },
        {
          id: 5,
          line: 'Да, говорят, еще какие!',
          correct: false,
          blank: false
        },
        {
          id: 6,
          line: 'Недаром помнит вся Россия',
          correct: false,
          blank: false
        },
        {
          id: 7,
          line: 'Про день Бородина!',
          correct: false,
          blank: true
        },
        {
          id: 8,
          line: '— Да, были люди в наше время,',
          correct: false,
          blank: false
        },
        {
          id: 9,
          line: 'Не то, что нынешнее племя:',
          correct: false,
          blank: false
        },
        {
          id: 10,
          line: 'Богатыри — не вы!',
          correct: false,
          blank: false
        },
        {
          id: 11,
          line: 'Плохая им досталась доля:',
          correct: false,
          blank: false
        },
        {
          id: 12,
          line: 'Немногие вернулись с поля…',
          correct: false,
          blank: false
        },
        {
          id: 13,
          line: 'Не будь на то господня воля,',
          correct: false,
          blank: false
        },
        {
          id: 14,
          line: 'Не отдали б Москвы!',
          correct: false,
          blank: true
        },
        {
          id: 15,
          line: 'Мы долго молча отступали,',
          correct: false,
          blank: false
        },
        {
          id: 16,
          line: 'Досадно было, боя ждали,',
          correct: false,
          blank: false
        },
        {
          id: 17,
          line: 'Ворчали старики:',
          correct: false,
          blank: false
        },
        {
          id: 18,
          line: '«Что ж мы? на зимние квартиры?',
          correct: false,
          blank: false
        },
        {
          id: 19,
          line: 'Не смеют, что ли, командиры',
          correct: false,
          blank: false
        },
        {
          id: 20,
          line: 'Чужие изорвать мундиры',
          correct: false,
          blank: false
        },
        {
          id: 21,
          line: 'О русские штыки?»',
          correct: false,
          blank: true
        }
      ],
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
    <div class="button--left base-flex">
      <button @click="prevClick" :disabled="!isPrevVisible">назад</button>
    </div>
    <div class="question">
      Стол {{ index + 1 }}
      <div class="table-container"><Table :question="questions[index]" /></div>
    </div>
    <div class="button--right base-flex">
      <button @click="nextClick" :disabled="!isNextVisible">вперёд</button>
    </div>
    <div class="rewards base-flex">
      <Inventory :inventory="inventory" />
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

.button--right {
  grid-column: 3;
  grid-row: 1;
}

.question {
  grid-column: 2;
  grid-row: 1;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
}

.table-container {
  width: 100%;
  height: 90%;
  margin: 4% 4% 0 4%;
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
