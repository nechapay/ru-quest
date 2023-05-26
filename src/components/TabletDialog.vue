<script setup>
import { onMounted, ref } from 'vue'
import _ from 'lodash'
import TabletAuth from './TabletAuth.vue'
import VerbPage from './VerbPage.vue'
import AuthorPage from './AuthorPage.vue'

const emits = defineEmits(['close', 'finished', 'completed'])
const props = defineProps(['tablet'])
function handleCloseClick() {
  emits('close')
}

let page = ref('')
let finished = ref(false)
let flowIndex = ref(0)

onMounted(() => {
  page.value = props.tablet.flow[flowIndex.value]
  finished.value = false
})

function nextStage() {
  if (flowIndex.value + 1 < props.tablet.flow.length) {
    flowIndex.value++
  } else {
    finished.value = true
    emits('finished')
  }
  page.value = props.tablet.flow[flowIndex.value]
}

function handleWorkClick(evt, val) {
  if (val.correct) {
    evt.target.classList.add('correct')
    nextStage()
  } else evt.target.classList.add('incorrect')
}

function handleLineClick(evt, val) {
  if (val.correct) {
    evt.target.classList.add('correct')
    nextStage()
  } else evt.target.classList.add('incorrect')
}

function handleTabletClick(evt) {
  let el = document.querySelector('.big-tablet').getBoundingClientRect()
  if (
    evt.offsetX >= el.width * 0.433 &&
    evt.offsetX <= el.width * 0.508 &&
    evt.offsetY >= el.height * 0.879 &&
    evt.offsetY <= el.height * 0.923
  ) {
    emits('close')
  }
}

function handleNumberClick(evt) {
  if (evt.target.value == props.tablet.numbers.correct) {
    evt.target.classList.add('correct')
    nextStage()
  } else {
    evt.target.classList.add('incorrect')
  }
}

function handleWordClick(evt, val) {
  if (val === props.tablet.word.correct) {
    evt.target.classList.add('correct')
    nextStage()
  } else evt.target.classList.add('incorrect')
}

function handleInfoClick() {
  emits('completed')
}
</script>

<template>
  <div class="dialog-wrapper fill base-flex" @click.self="handleCloseClick">
    <div class="dialog-body tablet big-tablet base-flex flex-column" @click.self="handleTabletClick">
      <Transition name="fade" mode="out-in">
        <div class="tablet-inner-wrapper" v-if="page === 'password'">
          <TabletAuth :password="tablet.password" @passed="nextStage" />
        </div>
        <AuthorPage :authors="tablet.authors" @finished="nextStage" v-else-if="page === 'authors'" />
        <div class="tablet-inner-wrapper" v-else-if="page === 'works'">
          <div
            class="work-wrapper"
            v-for="work in _.shuffle(tablet.works)"
            @click="handleWorkClick($event, work)"
            :id="`work_${work.id}`"
          >
            {{ work.name }}
          </div>
        </div>
        <div class="tablet-inner-wrapper flex-column no-wrap" v-else-if="page === 'poem'">
          <span class="base-flex fill">{{ tablet.poem.title }}</span>
          <hr />
          <div class="line-wrapper" v-for="item in tablet.poem.data">
            <span class="line-index">{{ item.id }}</span>
            <span class="line-text" @click="handleLineClick($event, item)">{{ item.line }}</span>
            <br v-if="item.blank" />
            <br />
          </div>
        </div>
        <div class="tablet-inner-wrapper flex-column no-wrap" v-else-if="page === 'numbers'">
          <span class="base-flex fill">{{ tablet.numbers.text }}</span>
          <hr />
          <div class="base-flex fill flex-wrap justify-start">
            <button
              class="tablet-number"
              v-for="number in tablet.numbers.count"
              :value="number"
              @click="handleNumberClick"
            >
              {{ number }}
            </button>
          </div>
        </div>
        <VerbPage :verb="tablet.verb" @finished="nextStage" :finished="finished" v-else-if="page === 'verb'" />
        <div class="tablet-inner-wrapper flex-column base-flex" v-else-if="page === 'info'">
          <span>{{ tablet?.info.text }}</span>

          <button class="tablet-number" @click="handleInfoClick">Приступить</button>
        </div>
        <div class="tablet-inner-wrapper flex-column base-flex" v-else-if="page === 'final'">
          <span>{{ tablet?.final.text }}</span>

          <button class="tablet-number" @click="handleInfoClick">Спастись</button>
        </div>
        <div class="tablet-inner-wrapper flex-column no-wrap" v-else-if="page === 'word'">
          <div class="line-wrapper" v-for="item in tablet.word.text">
            <span class="tablet-word" v-for="word in item.split(' ')" @click="handleWordClick($event, word)">{{
              word
            }}</span>
            <br />
          </div>
        </div>
      </Transition>
    </div>
  </div>
</template>

<style lang="css" scoped>
.dialog-wrapper {
  z-index: 2;
  position: fixed;
  top: 0;
  left: 0;
}

.dialog-body {
  height: 95%;
  font-size: 1.2em;
  text-align: justify;
}

.big-tablet {
  background: white;
  border: 2vh rgb(7, 80, 35) solid;
  border-top-width: 6vh;
  border-bottom-width: 7vh;
  border-radius: 2%;
}

.big-tablet:after {
  height: 6%;
  top: 104%;
}

.work-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 25%;
  cursor: pointer;
  border: 2px solid black;
  margin: 1%;
  text-align: center;
  padding: 1%;
  transition-duration: 0.5s;
  word-break: break-all;
}

.work-wrapper.correct {
  border: 2px solid rgb(3, 199, 3);
}

.work-wrapper.incorrect {
  border: 2px solid rgb(247, 89, 89);
  animation: tilt-shaking 0.15s;
}
.no-wrap {
  flex-wrap: nowrap;
}

.line-index {
  width: 24px;
  opacity: 0;
  display: inline-block;
  transition-duration: 0.5s;
}

.line-wrapper {
  cursor: pointer;
  user-select: none;
  margin: 4px 0;
  width: 100%;
}

.line-text {
  font-size: 100%;
}

.line-text.correct {
  color: rgb(3, 199, 3);
}

.line-text.incorrect {
  color: rgb(247, 89, 89);
  animation: tilt-shaking 0.15s;
}

.line-wrapper:hover .line-index {
  opacity: 1;
}

.tablet-number {
  font-size: 2rem;
  background: white;
  border: 1px solid green;
  transition-duration: 0.3s;
  padding: 2% 4%;
  min-width: 18%;
  margin: 0.5%;
  cursor: pointer;
}

.tablet-number:hover {
  background: green;
  color: white;
}

.tablet-number.correct {
  color: rgb(3, 199, 3);
}

.tablet-number.incorrect {
  color: rgb(247, 89, 89);
  animation: tilt-shaking 0.15s;
}

.tablet-word {
  margin-right: 8px;
}

.tablet-word.correct {
  color: rgb(3, 199, 3);
}

.tablet-word.incorrect {
  color: rgb(247, 89, 89);
  animation: tilt-shaking 0.15s;
}
</style>
