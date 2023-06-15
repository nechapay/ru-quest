<script setup>
import { onMounted, ref } from 'vue'
import DragWord from './DragWord.vue'
import Intro from './Intro.vue'

const emits = defineEmits(['completed'])
const props = defineProps(['question'])

let faded = ref(false)
const introVisible = ref(false)
const showFinalMessage = ref(false)

onMounted(() => {
  setTimeout(() => {
    introVisible.value = true
    faded.value = true
  }, 300)
})

function handleDragWordCompleted() {
  showFinalMessage.value = true
}

function handleIntroClose() {
  introVisible.value = false
  faded.value = false
}
</script>
<template>
  <div class="table final-table base-flex flex-column fill">
    <Transition name="bounce">
      <div class="tablet-landscape">
        <video controls>
          <source src="/video/block.mp4" type="video/mp4" />
          <track label="Русский" kind="subtitles" srclang="ru" src="/video/block.vtt" default />
        </video>
      </div>
    </Transition>
    <DragWord :correct="question.correct" @completed="handleDragWordCompleted" />
    <Transition name="fade"><div class="transparent-fader fill" v-if="faded"></div></Transition>
    <Transition name="bounce">
      <Intro :value="question.intro" v-if="introVisible" @close="handleIntroClose" />
      <Intro :value="question.reward" v-else-if="showFinalMessage" @close="emits('completed')" />
    </Transition>
  </div>
</template>
<style scoped>
.final-table {
  height: 130%;
  z-index: 2;
  padding-top: 2%;
}

.tablet-landscape {
  position: relative;
  height: 40vh;
  border: 1vh rgb(7, 80, 35) solid;
  border-left-width: 3vh;
  border-right-width: 5vh;
  border-radius: 8px;
  aspect-ratio: 8/5;
  background: #333;
}

.tablet-landscape:after {
  content: '';
  display: block;
  height: 10%;
  position: absolute;
  right: -9%;
  top: 50%;
  transform: translate(-50%, -50%);
  background: #333;
  border-radius: 50%;
  border: 0.5vh solid rgb(77 157 28);
  aspect-ratio: 1/1;
}

.tablet-landscape video {
  height: 100%;
}
</style>
