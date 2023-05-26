<script setup>
import { computed, ref, watch } from 'vue'
import Table from './Table.vue'
import Inventory from './Inventory.vue'

const emits = defineEmits(['ended'])

const questions = [
  {
    id: 'q_1',
    lastStage: false,
    scroll: {
      type: 'list',
      text: 'Итак, А.С. Пушкин. На смерть этого поэта другое «юное дарование» <b>(Х)</b> пишет стихотворение и за него ссылается на Кавказ.',
      list: [
        'Этот поэт <b>(Х)</b> на 25-летие важной исторической битвы пишет балладу <b>(Y)</b>.',
        'Этот поэт <b>(Х)</b> прожил очень мало. Он родился через 2 года после описываемого им в балладе <b>(Y)</b> сражения. Во время восстания декабристов ему было 11 лет.',
        'Даты его рождения и смерти легко запоминаются: последние две цифры зеркальны. Посчитайте, сколько же лет прожил поэт <b>(Х)</b> и отсчитайте в его балладе <b>(Y)</b> стих под таким номером.',
        'Пароль к планшету : <b>1847</b>'
      ]
    },
    tablet: {
      flow: ['password', 'authors', 'works', 'poem', 'verb'],
      password: {
        correct: '1847'
      },
      authors: [
        {
          id: 1,
          name: 'Ахматова',
          img: 'Akhmatova.jpg',
          correct: false
        },
        {
          id: 2,
          name: 'Блок',
          img: 'Blok.jpg',
          correct: false
        },
        {
          id: 3,
          name: 'Есенин',
          img: 'Esenin.jpg',
          correct: false
        },
        {
          id: 4,
          name: 'Лермонтов',
          img: 'Lermontov.jpg',
          correct: true
        },
        {
          id: 5,
          name: 'Маяковский',
          img: 'Mayakovsky.jpg',
          correct: false
        },
        {
          id: 6,
          name: 'Некрасов',
          img: 'Nekrasov.jpg',
          correct: false
        },
        {
          id: 7,
          name: 'Пушкин',
          img: 'Pushkin.jpg',
          correct: false
        },
        {
          id: 8,
          name: 'Твардовский',
          img: 'Tvardovsky.jpg',
          correct: false
        }
      ],
      works: [
        {
          id: 1,
          name: 'Морская царевна',
          correct: false
        },
        {
          id: 2,
          name: 'Воздушный корабль',
          correct: false
        },
        {
          id: 3,
          name: 'Пир Асмодея',
          correct: false
        },
        {
          id: 4,
          name: 'Мрак. Тьма',
          correct: false
        },
        {
          id: 5,
          name: 'Бородино',
          correct: true
        },
        {
          id: 6,
          name: 'Джюлио',
          correct: false
        },
        {
          id: 7,
          name: 'Прощание Наполеона',
          correct: false
        },
        {
          id: 8,
          name: 'Три ведьмы',
          correct: false
        }
      ],
      poem: {
        title: 'Лермонтов. Бородино.',
        data: [
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
            correct: true,
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
        ]
      },
      verb: {
        title:
          'А теперь немного из программы Русского языка: найдите в этой строке букву, использующуюся 1 раз и характеризующуюся как согласный звук, мягкий парный, глухой парный.',
        pre: '…',
        main: 'и леса синие верхушки',
        post: '.',
        reward: 'К',
        correct: 'к',
        message: ''
      }
    }
  },
  {
    id: 'q_2',
    lastStage: false,
    scroll: {
      type: 'list',
      text: 'Описание этого сражения <b>(Y)</b> есть ещё у одного известного писателя <b>(L)</b>; только теперь картина битвы представлена в прозе, в романе-эпопее.',
      list: [
        'Примечательно, что у этого писателя <b>(L)</b> и у А.С.Пушкина есть произведения с одинаковыми названиями. И в этом названии <b>(М)</b> одно из слов – однокоренное с местом ссылки нашего поэта <b>(Х)</b>.',
        'Чтобы найти вторую букву, вам необходимо вспомнить главного героя произведения <b>(L)</b>, чьи мужество и стойкость, ум и сила вызывают восхищение читателя.',
        'Из его фамилии нужно забрать букву, выраженную согласным звуком, сонорным мягким парным.',
        'Пароль к планшету : <b>2042</b>'
      ]
    },
    tablet: {
      flow: ['password', 'authors', 'works', 'poem', 'verb'],
      password: {
        correct: '2042'
      },
      authors: [
        {
          id: 1,
          name: '',
          img: 'q2author1.jpg',
          correct: false
        },
        {
          id: 2,
          name: '',
          img: 'q2author2.jpg',
          correct: false
        },
        {
          id: 3,
          name: '',
          img: 'q2author3.jpg',
          correct: false
        },
        {
          id: 4,
          name: '',
          img: 'q2author4.jpg',
          correct: true
        },
        {
          id: 5,
          name: '',
          img: 'q2author5.jpg',
          correct: false
        },
        {
          id: 6,
          name: '',
          img: 'q2author6.jpg',
          correct: false
        },
        {
          id: 7,
          name: '',
          img: 'q2author7.jpg',
          correct: false
        },
        {
          id: 8,
          name: '',
          img: 'q2author8.jpg',
          correct: false
        }
      ],
      works: [
        {
          id: 1,
          name: 'Бедные люди',
          correct: false
        },
        {
          id: 2,
          name: 'Разжалованный',
          correct: false
        },
        {
          id: 3,
          name: 'Суратская кофейная',
          correct: false
        },
        {
          id: 4,
          name: 'Записки маркёра',
          correct: false
        },
        {
          id: 5,
          name: 'Кавказский пленник',
          correct: true
        },
        {
          id: 6,
          name: 'Поликушка',
          correct: false
        },
        {
          id: 7,
          name: 'Записки сумасшедшего',
          correct: false
        },
        {
          id: 8,
          name: 'Хаджи-Мурат',
          correct: false
        }
      ],
      poem: {
        title: 'Толстой. Кавказский пленник.',
        data: [
          {
            id: 1,
            line: 'Курагин',
            correct: false,
            blank: true
          },
          {
            id: 2,
            line: 'Болконский',
            correct: false,
            blank: true
          },
          {
            id: 3,
            line: 'Каренина',
            correct: false,
            blank: true
          },
          {
            id: 4,
            line: 'Ростов',
            correct: false,
            blank: true
          },
          {
            id: 5,
            line: 'Каратаев',
            correct: false,
            blank: true
          },
          {
            id: 6,
            line: 'Друбецкая',
            correct: false,
            blank: true
          },
          {
            id: 7,
            line: 'Жилин',
            correct: true,
            blank: true
          },
          {
            id: 8,
            line: 'Перфильев',
            correct: false,
            blank: true
          },
          {
            id: 9,
            line: 'Облонский',
            correct: false,
            blank: true
          },
          {
            id: 10,
            line: 'Нехлюдов',
            correct: false,
            blank: true
          },
          {
            id: 11,
            line: 'Касатский',
            correct: false,
            blank: true
          }
        ]
      },
      verb: {
        title:
          'А теперь немного из программы Русского языка: нужно найти букву, выраженную согласным звуком, сонорным мягким парным.',
        pre: '',
        main: 'Жилин',
        post: '',
        reward: 'Л',
        correct: 'л',
        message: ''
      }
    }
  },
  {
    id: 'q_3',
    lastStage: false,
    scroll: {
      type: 'list',
      text: 'На берегу пустынных волн<br>Стоял ОН, дум высоких полн…<br>Эти строки из поэмы А.С.Пушкина «Медный всадник». В Петербурге, недалеко от Исаакиевского собора, стоит тот памятник, название которого вынес Пушкин в заголовок.',
      list: [
        'Вспомните фамилию первого русского императора.',
        'Заберите из этой фамилии букву, повторяющуюся дважды.',
        'Пароль к планшету : <b>1701</b>'
      ]
    },
    tablet: {
      flow: ['password', 'authors', 'poem', 'verb'],
      password: {
        correct: '1701'
      },
      authors: [
        {
          id: 1,
          name: 'Александр III',
          img: 'q3_1.jpg',
          correct: false
        },
        {
          id: 2,
          name: 'Пётр III',
          img: 'q3_2.jpg',
          correct: false
        },
        {
          id: 3,
          name: 'Александр II',
          img: 'q3_3.jpg',
          correct: false
        },
        {
          id: 4,
          name: 'Николай I',
          img: 'q3_4.jpg',
          correct: false
        },
        {
          id: 5,
          name: 'Николай II',
          img: 'q3_5.jpg',
          correct: false
        },
        {
          id: 6,
          name: 'Пётр I',
          img: 'q3_6.jpg',
          correct: true
        },
        {
          id: 7,
          name: 'Павел I',
          img: 'q3_7.jpg',
          correct: false
        },
        {
          id: 8,
          name: 'Александр I',
          img: 'q3_8.jpg',
          correct: false
        }
      ],
      poem: {
        title: 'Пётр I.',
        data: [
          {
            id: 1,
            line: 'Годунов',
            correct: false,
            blank: true
          },
          {
            id: 2,
            line: 'Романов',
            correct: true,
            blank: true
          },
          {
            id: 3,
            line: 'Шуйский',
            correct: false,
            blank: true
          },
          {
            id: 4,
            line: 'Рюрикович',
            correct: false,
            blank: true
          },
          {
            id: 5,
            line: 'Ульянов',
            correct: false,
            blank: true
          },
          {
            id: 6,
            line: 'Джугашвили',
            correct: false,
            blank: true
          }
        ]
      },
      verb: {
        title: 'Заберите из этой фамилии букву, повторяющуюся дважды.',
        pre: '',
        main: 'Романов',
        post: '',
        reward: 'О',
        correct: 'о',
        message: ''
      }
    }
  },
  {
    id: 'q_4',
    lastStage: false,
    scroll: {
      type: 'list',
      text: 'Четвёртую  букву вы можете найти:',
      list: [
        'в названии одного из родовых имений Пушкиных;',
        'в одном из отгаданных в сегодняшнем квесте слов;',
        'в названии одного из городов-героев;',
        'в названиях трёх знаменитых произведений И.А.Гончарова;',
        'в одной из первых фраз переродившегося из собаки Шарикова, да и в названии самого этого произведения; и даже в фамилии автора;',
        'в названии дерева – символа России;',
        'в названии города, над которым 1 мая  1945 взметнулся штурмовой флаг 150-й ордена Кутузова II степени Идрицкой  стрелковой дивизии.',
        'Пароль к планшету : <b>2150</b>'
      ]
    },
    tablet: {
      flow: ['password', 'verb'],
      password: {
        correct: '2150'
      },
      verb: {
        title: 'Найдите букву из подсказок',
        pre: '',
        main: 'Болдино Бородино Брест «Обрыв» «Обломов» «Обыкновенная история» «АБЫРВАЛГ» «Собачье сердце» Булгаков берёза Берлин',
        post: '',
        reward: 'Б',
        correct: 'б',
        message: ''
      }
    }
  },
  {
    id: 'q_5',
    lastStage: true,
    scroll: {
      type: 'list',
      text: 'Пятую подсказку вы найдёте путём вычислений:',
      list: [
        'от цифры, обозначающей год начала Второй мировой войны, отнять цифру, обозначающую год окончания Первой мировой войны;',
        'к полученной цифре добавьте цифру, обозначающую год отмены крепостного права;',
        'от полученной цифры отнимите число, обозначающее год битвы под Бородином;',
        'к полученной цифре добавьте цифру, обозначающую год восстания декабристов на Сенатской площади в Петербурге;',
        'к полученному числу прибавьте цифру, обозначающую год крещения Руси Владимиром;',
        'от полученного числа отнимите цифру, обозначающую год, когда произошла Невская битва (ледовое побоище);',
        'из полученного числа вычтите цифру, обозначающую год начала правления династии Романовых (после смуты).',
        'Пароль к планшету: <b>РЕЗУЛЬТАТ ВЫЧИСЛЕНИЙ</b>'
      ]
    },
    tablet: {
      flow: ['password', 'info'],
      password: {
        correct: '28'
      },
      info: {
        text: 'Вы нашли 4 буквы и цифру. Из 4-х букв вы должны сложить фамилию поэта-символиста начала 20 века. Именно в сборнике его стихов (на полке кабинета), на странице, номер которой вы только что нашли, вы можете обнаружить нужный вам КЛЮЧ!!! КЛЮЧ представляет собой строчку, которую вы должны сообщить в качестве пароля ведущему. Узнайте эту строку по подсказкам (на странице).'
      }
    }
  }
]

const final = {
  id: 'final_1',
  scroll: {
    type: 'list',
    text: 'Вы нашли 4 буквы и цифру. Из 4-х букв вы должны сложить фамилию поэта-символиста начала 20 века. Именно в сборнике его стихов (на полке кабинета), на странице, номер которой вы только что нашли, вы можете обнаружить нужный вам КЛЮЧ!!! КЛЮЧ представляет собой строчку, которую вы должны сообщить в качестве пароля ведущему. Узнайте эту строку по подсказкам (на странице).',
    list: [
      'НАЗВАНИЕ ОДНОГО ИЗ ПРОИЗВЕДЕНИЙ А.Н.ОСТРОВСКОГО',
      'ОДНОКОРЕННОЕ С ОДНИМ ИЗ СЛОВ ИСТОРИЧЕСКОГО СЛОВОСОЧЕТАНИЯ «ДЕКАБРИСТСКОЕ ВОССТАНИЕ»',
      'ИМЕННО ЭТО РАЗРАЗИЛОСЬ НАД МОСКВОЙ, ИЗОБРАЖЁННОЙ БУЛГАКОВЫМ, КОГДА ЕЁ ПОКИДАЛА СВИТА ВОЛАНДА'
    ]
  },
  tablet: {
    flow: ['authors', 'numbers', 'word', 'final'],
    authors: [
      {
        id: 1,
        name: 'Ахматова',
        img: 'Akhmatova.jpg',
        correct: false
      },
      {
        id: 2,
        name: 'Блок',
        img: 'Blok.jpg',
        correct: true
      },
      {
        id: 3,
        name: 'Есенин',
        img: 'Esenin.jpg',
        correct: false
      },
      {
        id: 4,
        name: 'Лермонтов',
        img: 'Lermontov.jpg',
        correct: false
      },
      {
        id: 5,
        name: 'Маяковский',
        img: 'Mayakovsky.jpg',
        correct: false
      },
      {
        id: 6,
        name: 'Некрасов',
        img: 'Nekrasov.jpg',
        correct: false
      },
      {
        id: 7,
        name: 'Пушкин',
        img: 'Pushkin.jpg',
        correct: false
      },
      {
        id: 8,
        name: 'Твардовский',
        img: 'Tvardovsky.jpg',
        correct: false
      }
    ],
    numbers: {
      text: 'Выберите номер страницы',
      correct: 28,
      count: 99
    },
    word: {
      text: ['гроза заря удар'],
      correct: 'гроза'
    },
    final: {
      text: 'Вы выбрались! Дверь открыта!'
    }
  }
}

const inventory = ref([
  {
    id: 0,
    name: ''
  },
  {
    id: 1,
    name: ''
  },
  {
    id: 2,
    name: ''
  },
  {
    id: 3,
    name: ''
  }
])

const index = ref(0)
const finalStage = ref(false)
const enableDrag = ref(false)

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
  return index.value < questions.length - 1 && allowNextStage.value
})

function putReward() {
  inventory.value[index.value].name = questions[index.value].tablet.verb.reward
}

function handleTableFinished() {
  putReward()
}

function handleCompleted() {
  if (finalStage.value) {
    emits('ended')
  }
  enableDrag.value = true
}

let allowNextStage = computed(() => {
  if (index.value < inventory.value.length && inventory.value[index.value].name !== '') {
    return true
  }
  return false
})

let answer = computed(() => {
  let str = inventory.value.map((i) => i.name).join('')
  return str
})

watch(answer, (newValue, oldValue) => {
  if (newValue === 'БЛОК') {
    finalStage.value = true
    enableDrag.value = false
  } else if (newValue.length === 4 && !finalStage.value) {
    enableDrag.value = true
  }
})
</script>
<template>
  <div class="main-page-container my-grid">
    <div class="button--left base-flex">
      <button class="nav-button" @click="prevClick" :disabled="!isPrevVisible" v-if="!finalStage" title="предыдущий">
        &lt
      </button>
    </div>
    <div class="question">
      <span class="table-index" v-if="!finalStage">СТОЛ {{ index + 1 }}</span>
      <div class="table-container">
        <Transition name="fade" mode="out-in">
          <Table
            :question="questions[index]"
            @finished="handleTableFinished"
            :key="questions[index].id"
            @completed="handleCompleted"
            v-if="!finalStage"
          />
          <Table
            :question="final"
            @finished="handleTableFinished"
            :key="final.id"
            @completed="handleCompleted"
            v-else-if="finalStage"
          />
        </Transition>
      </div>
    </div>
    <div class="button--right base-flex">
      <button class="nav-button" @click="nextClick" :disabled="!isNextVisible" v-if="!finalStage" title="следующий">
        &gt
      </button>
    </div>
    <div class="rewards base-flex">
      <Inventory :inventory="inventory" :enabled="enableDrag" />
    </div>
  </div>
</template>

<style scoped>
.main-page-container {
  width: 90%;
  height: 90%;
  margin: 2% 5%;
  border: 1px solid black;
  background: linear-gradient(to bottom, #f7fbfc 0%, #d9edf2 40%, #add9e4 100%);
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
  margin: 2% 4% 0 4%;
}
.rewards {
  grid-row: 2;
  grid-column: 1/4;
}

.list-group {
  display: flex;
}

.table-index {
  margin-top: 2%;
  font-size: 200%;
  font-family: EchoRevival, serif;
}

.nav-button {
  font-size: 4rem;
  background: white;
  border: 1px solid grey;
  transition-duration: 0.3s;
  padding: 20% 2%;
}

.nav-button:enabled {
  border: 1px solid green;
}

.nav-button:hover:enabled {
  background: green;
  color: white;
}
</style>
