<script setup>
import { onMounted, ref } from 'vue'
import _ from 'lodash'
const emits = defineEmits(['close', 'finished'])
const props = defineProps(['tablet'])
function handleCloseClick() {
  emits('close')
}

let page = ref('')
let author = ref('')
let work = ref('')
let finished = ref(false)
let flowIndex = ref(0)

onMounted(() => {
  page.value = props.tablet.flow[flowIndex.value]
})

function nextStage() {
  if (flowIndex.value + 1 < props.tablet.flow.length) {
    flowIndex.value++
  }
  page.value = props.tablet.flow[flowIndex.value]
}

function handleAuthorClick(evt, val) {
  let element = document.getElementById('auth_' + evt.target.id.split('_')[1])
  if (val.correct) {
    element.classList.add('correct')
    author.value = val.name
    nextStage()
  } else element.classList.add('incorrect')
}

function handleWorkClick(evt, val) {
  if (val.correct) {
    evt.target.classList.add('correct')
    work.value = val.name
    nextStage()
  } else evt.target.classList.add('incorrect')
}

function handleLineClick(evt, val) {
  if (val.correct) {
    evt.target.classList.add('correct')
    nextStage()
  } else evt.target.classList.add('incorrect')
}

function handleLetterClick(evt, val) {
  if (val === ' ') return
  if (val === props.tablet.verb.correct) {
    evt.target.classList.add('correct')
    finished.value = true
    emits('finished')
  } else evt.target.classList.add('incorrect')
}
</script>

<template>
  <div class="dialog-wrapper fill base-flex" @click.self="handleCloseClick">
    <div class="dialog-body big-tablet base-flex flex-column">
      <Transition name="fade" mode="out-in">
        <div class="tablet-inner-wrapper" v-if="page === 'authors'">
          <div
            class="author-wrapper"
            v-for="item in _.shuffle(tablet.authors)"
            @click="handleAuthorClick($event, item)"
            :id="`auth_${item.id}`"
          >
            <img :src="`./img/${item.img}`" :id="`img_${item.id}`" />
            <span>{{ item.name }}</span>
          </div>
        </div>
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
          {{ author }}. {{ work }}
          <hr />
          <div class="line-wrapper" v-for="item in tablet.poem">
            <span class="line-index">{{ item.id }}</span>
            <span class="line-text" @click="handleLineClick($event, item)">{{ item.line }}</span>
            <br v-if="item.blank" />
            <br />
          </div>
        </div>
        <div class="tablet-inner-wrapper justify-center" v-else-if="page === 'verb'">
          {{ tablet?.verb.title }}
          <span class="verb-letter blank">{{ tablet?.verb.pre }}</span>
          <span
            class="verb-letter"
            :class="{ blank: item === ' ' }"
            @click="handleLetterClick($event, item)"
            v-for="item in tablet.verb.main.split('')"
            >{{ item }}</span
          >
          <span class="verb-letter blank">{{ tablet?.verb.post }}</span>
          <Transition name="fade">
            <div v-if="finished">message</div>
          </Transition>
        </div>
      </Transition>
      <button class="tablet-close-button" @click="handleCloseClick" title="Закрыть"></button>
    </div>
  </div>
</template>

<style lang="css" scoped>
.dialog-wrapper {
  z-index: 2;
  position: fixed;
  top: 0;
  left: 0;
  /* background: rgba(128, 128, 128, 0.425); */
}

.dialog-body {
  width: 38%;
  height: 95%;
  padding: 2%;
  font-size: 1.2em;
  text-align: justify;
}

.big-tablet {
  background-image: url('/img/tablet.png');
  background-repeat: no-repeat;
  background-size: cover;
  width: 37.1%;
  min-height: 240px;
  min-width: 172px;
}

.tablet-inner-wrapper {
  display: flex;
  flex-wrap: wrap;
  overflow-y: scroll;
  overflow-x: hidden;
  /* border: 1px solid black; */
  width: 98%;
  height: 89%;
  margin-top: 8%;
  padding: 2%;
}

.tablet-inner-wrapper::-webkit-scrollbar {
  width: 10px;
}

.tablet-inner-wrapper::-webkit-scrollbar-track {
  background-color: #5c5a5a3f;
  border-radius: 100px;
}

.tablet-inner-wrapper::-webkit-scrollbar-thumb {
  background-color: rgb(151, 148, 148);
  border-radius: 100px;
}

.tablet-close-button {
  padding: 4%;
  border-radius: 50%;
  border: 4px solid #362727;
  position: relative;
  top: 3%;
  background: white;
  cursor: pointer;
}

.author-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  max-width: 35%;
  height: auto;
  padding: 1%;
  margin: 2%;
  cursor: pointer;
  border: 2px solid transparent;
  transition-duration: 0.5s;
}

.author-wrapper.correct {
  border: 2px solid rgb(3, 199, 3);
}

.author-wrapper.incorrect {
  border: 2px solid rgb(247, 89, 89);
}

.author-wrapper img {
  max-width: 100%;
  height: 95%;
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
}

.work-wrapper.correct {
  border: 2px solid rgb(3, 199, 3);
}

.work-wrapper.incorrect {
  border: 2px solid rgb(247, 89, 89);
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
  width: 80%;
}

.line-text.correct {
  color: rgb(3, 199, 3);
}

.line-text.incorrect {
  color: rgb(247, 89, 89);
}

.line-wrapper:hover .line-index {
  opacity: 1;
}

.verb-letter {
  display: inline-block;
  min-width: 8px;
  font-size: 2rem;
  cursor: pointer;
  user-select: none;
}

.verb-letter.correct {
  color: rgb(3, 199, 3);
  cursor: auto;
  font-weight: bolder;
}

.verb-letter.incorrect {
  color: rgb(247, 89, 89);
  cursor: auto;
  font-weight: bolder;
}

.verb-letter:hover {
  font-weight: bolder;
}

.verb-letter.blank {
  cursor: auto;
}

.verb-letter.blank:hover {
  font-weight: 100;
}
</style>
