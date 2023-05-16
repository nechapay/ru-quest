<script setup>
import { computed, onMounted, ref } from 'vue'
import draggable from 'vuedraggable'
import Table from './Table.vue'
import Inventory from './Inventory.vue'

const questions = [
  {
    scroll: {
      type: 'list',
      text: 'Итак, А.С.Пушкин. На смерть этого поэта другое «юное дарование» <b>(Х)</b> пишет стихотворение и за него ссылается на Кавказ.',
      list: [
        'Этот поэт <b>(Х)</b> на 25-летие важной исторической битвы пишет балладу <b>(Y)</b>.',
        'Этот поэт <b>(Х)</b> прожил очень мало. Он родился через 2 года после описываемого им в балладе <b>(Y)</b> сражения. Во время восстания декабристов ему было 11 лет.',
        'Даты его рождения и смерти легко запоминаются: последние две цифры зеркальны. Посчитайте, сколько же лет прожил поэт <b>(Х)</b> и отсчитайте в его балладе <b>(Y)</b> стих под таким номером.'
      ]
    },
    tablet: {
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
          },
          {
            id: 22,
            line: 'И вот нашли большое поле:',
            correct: false,
            blank: false
          },
          {
            id: 23,
            line: 'Есть разгуляться где на воле!',
            correct: false,
            blank: false
          },
          {
            id: 24,
            line: 'Построили редут.',
            correct: false,
            blank: false
          },
          {
            id: 25,
            line: 'У наших ушки на макушке!',
            correct: false,
            blank: false
          },
          {
            id: 26,
            line: 'Чуть утро осветило пушки',
            correct: false,
            blank: false
          },
          {
            id: 27,
            line: 'И леса синие верхушки —',
            correct: false,
            blank: false
          },
          {
            id: 28,
            line: 'Французы тут как тут.',
            correct: false,
            blank: true
          },
          {
            id: 29,
            line: 'Забил заряд я в пушку туго',
            correct: false,
            blank: false
          },
          {
            id: 30,
            line: 'И думал: угощу я друга!',
            correct: false,
            blank: false
          },
          {
            id: 31,
            line: 'Постой-ка, брат мусью!',
            correct: false,
            blank: false
          },
          {
            id: 32,
            line: 'Что тут хитрить, пожалуй к бою;',
            correct: false,
            blank: false
          },
          {
            id: 33,
            line: 'Уж мы пойдем ломить стеною,',
            correct: false,
            blank: false
          },
          {
            id: 34,
            line: 'Уж постоим мы головою',
            correct: false,
            blank: false
          },
          {
            id: 35,
            line: 'За родину свою!',
            correct: false,
            blank: true
          },
          {
            id: 36,
            line: 'Два дня мы были в перестрелке.',
            correct: false,
            blank: false
          },
          {
            id: 37,
            line: 'Что толку в этакой безделке?',
            correct: false,
            blank: false
          },
          {
            id: 38,
            line: 'Мы ждали третий день.',
            correct: false,
            blank: false
          },
          {
            id: 39,
            line: 'Повсюду стали слышны речи:',
            correct: false,
            blank: false
          },
          {
            id: 40,
            line: '«Пора добраться до картечи!»',
            correct: false,
            blank: false
          },
          {
            id: 41,
            line: 'И вот на поле грозной сечи',
            correct: false,
            blank: false
          },
          {
            id: 42,
            line: 'Ночная пала тень.',
            correct: false,
            blank: true
          },
          {
            id: 43,
            line: 'Прилег вздремнуть я у лафета,',
            correct: false,
            blank: false
          },
          {
            id: 44,
            line: 'И слышно было до рассвета,',
            correct: false,
            blank: false
          },
          {
            id: 45,
            line: 'Как ликовал француз.',
            correct: false,
            blank: false
          },
          {
            id: 46,
            line: 'Но тих был наш бивак открытый:',
            correct: false,
            blank: false
          },
          {
            id: 47,
            line: 'Кто кивер чистил весь избитый,',
            correct: false,
            blank: false
          },
          {
            id: 48,
            line: 'Кто штык точил, ворча сердито,',
            correct: false,
            blank: false
          },
          {
            id: 49,
            line: 'Кусая длинный ус.',
            correct: false,
            blank: true
          },
          {
            id: 50,
            line: 'И только небо засветилось,',
            correct: false,
            blank: false
          },
          {
            id: 51,
            line: 'Все шумно вдруг зашевелилось,',
            correct: false,
            blank: false
          },
          {
            id: 52,
            line: 'Сверкнул за строем строй.',
            correct: false,
            blank: false
          },
          {
            id: 53,
            line: 'Полковник наш рожден был хватом:',
            correct: false,
            blank: false
          },
          {
            id: 54,
            line: 'Слуга царю, отец солдатам…',
            correct: false,
            blank: false
          },
          {
            id: 55,
            line: 'Да, жаль его: сражен булатом,',
            correct: false,
            blank: false
          },
          {
            id: 56,
            line: 'Он спит в земле сырой.',
            correct: false,
            blank: true
          },
          {
            id: 57,
            line: 'И молвил он, сверкнув очами:',
            correct: false,
            blank: false
          },
          {
            id: 58,
            line: '«Ребята! не Москва ль за нами?',
            correct: false,
            blank: false
          },
          {
            id: 59,
            line: 'Умремте ж под Москвой,',
            correct: false,
            blank: false
          },
          {
            id: 60,
            line: 'Как наши братья умирали!»',
            correct: false,
            blank: false
          },
          {
            id: 61,
            line: 'И умереть мы обещали,',
            correct: false,
            blank: false
          },
          {
            id: 62,
            line: 'И клятву верности сдержали',
            correct: false,
            blank: false
          },
          {
            id: 63,
            line: 'Мы в Бородинский бой.',
            correct: false,
            blank: true
          },
          {
            id: 64,
            line: 'Ну ж был денек! Сквозь дым летучий',
            correct: false,
            blank: false
          },
          {
            id: 65,
            line: 'Французы двинулись, как тучи,',
            correct: false,
            blank: false
          },
          {
            id: 66,
            line: 'И всё на наш редут.',
            correct: false,
            blank: false
          },
          {
            id: 67,
            line: 'Уланы с пестрыми значками,',
            correct: false,
            blank: false
          },
          {
            id: 68,
            line: 'Драгуны с конскими хвостами,',
            correct: false,
            blank: false
          },
          {
            id: 69,
            line: 'Все промелькнули перед нами,',
            correct: false,
            blank: false
          },
          {
            id: 70,
            line: 'Все побывали тут.',
            correct: false,
            blank: true
          },
          {
            id: 71,
            line: 'Вам не видать таких сражений!..',
            correct: false,
            blank: false
          },
          {
            id: 72,
            line: 'Носились знамена, как тени,',
            correct: false,
            blank: false
          },
          {
            id: 73,
            line: 'В дыму огонь блестел,',
            correct: false,
            blank: false
          },
          {
            id: 74,
            line: 'Звучал булат, картечь визжала,',
            correct: false,
            blank: false
          },
          {
            id: 75,
            line: 'Рука бойцов колоть устала,',
            correct: false,
            blank: false
          },
          {
            id: 76,
            line: 'И ядрам пролетать мешала',
            correct: false,
            blank: false
          },
          {
            id: 77,
            line: 'Гора кровавых тел.',
            correct: false,
            blank: true
          },
          {
            id: 78,
            line: 'Изведал враг в тот день немало,',
            correct: false,
            blank: false
          },
          {
            id: 79,
            line: 'Что значит русский бой удалый,',
            correct: false,
            blank: false
          },
          {
            id: 80,
            line: 'Наш рукопашный бой!..',
            correct: false,
            blank: false
          },
          {
            id: 81,
            line: 'Земля тряслась — как наши груди,',
            correct: false,
            blank: false
          },
          {
            id: 82,
            line: 'Смешались в кучу кони, люди,',
            correct: false,
            blank: false
          },
          {
            id: 83,
            line: 'И залпы тысячи орудий',
            correct: false,
            blank: false
          },
          {
            id: 84,
            line: 'Слились в протяжный вой…',
            correct: false,
            blank: true
          },
          {
            id: 85,
            line: 'Вот смерклось. Были все готовы',
            correct: false,
            blank: false
          },
          {
            id: 86,
            line: 'Заутра бой затеять новый',
            correct: false,
            blank: false
          },
          {
            id: 87,
            line: 'И до конца стоять…',
            correct: false,
            blank: false
          },
          {
            id: 88,
            line: 'Вот затрещали барабаны —',
            correct: false,
            blank: false
          },
          {
            id: 89,
            line: 'И отступили бусурманы.',
            correct: false,
            blank: false
          },
          {
            id: 90,
            line: 'Тогда считать мы стали раны,',
            correct: false,
            blank: false
          },
          {
            id: 91,
            line: 'Товарищей считать.',
            correct: false,
            blank: true
          },
          {
            id: 92,
            line: 'Да, были люди в наше время,',
            correct: false,
            blank: false
          },
          {
            id: 93,
            line: 'Могучее, лихое племя:',
            correct: false,
            blank: false
          },
          {
            id: 94,
            line: 'Богатыри — не вы.',
            correct: false,
            blank: false
          },
          {
            id: 95,
            line: 'Плохая им досталась доля:',
            correct: false,
            blank: false
          },
          {
            id: 96,
            line: 'Немногие вернулись с поля.',
            correct: false,
            blank: false
          },
          {
            id: 97,
            line: 'Когда б на то не божья воля,',
            correct: false,
            blank: false
          },
          {
            id: 98,
            line: 'Не отдали б Москвы!',
            correct: false,
            blank: true
          },
          {
            id: 98,
            line: '1837 г.',
            correct: false,
            blank: false
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

.list-group {
  display: flex;
}
</style>
