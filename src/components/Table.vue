<script setup>
import { computed, onMounted, ref } from 'vue'
import TabletDialog from './TabletDialog.vue'
import ScrollDialog from './ScrollDialog.vue'
import Intro from './Intro.vue'

const props = defineProps(['question'])
const emits = defineEmits(['finished', 'completed'])
let faded = ref(false)

let tabletDialogVisible = ref(false)
let scrollDialogVisible = ref(false)
const introVisible = ref(false)

const tabletVisible = computed(() => !tabletDialogVisible.value)

function showDialog(dialog, val) {
  if (!dialog) return
  if (dialog === 'tablet') tabletDialogVisible.value = val
  if (dialog === 'scroll') scrollDialogVisible.value = val
  faded.value = val
}

function handleCompleted() {
  tabletDialogVisible.value = false
  emits('completed')
}

function handleIntroClose() {
  introVisible.value = false
  faded.value = false
}

onMounted(() => {
  setTimeout(() => {
    introVisible.value = true
    faded.value = true
  }, 300)
})
</script>
<template>
  <div class="table fill">
    <Transition name="bounce">
      <div class="scroll base-flex flex-column" @click="showDialog('scroll', true)">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
    </Transition>
    <Transition name="bounce">
      <div class="tablet" @click="showDialog('tablet', true)" v-show="tabletVisible"></div>
    </Transition>
    <Transition name="fade"><div class="transparent-fader fill" v-if="faded"></div></Transition>
    <Transition name="bounce">
      <ScrollDialog v-if="scrollDialogVisible" @close="showDialog('scroll', false)" :scroll="question?.scroll" />
    </Transition>
    <Transition name="bounce">
      <TabletDialog
        v-if="tabletDialogVisible"
        @close="showDialog('tablet', false)"
        :tablet="question?.tablet"
        @finished="(e) => emits('finished')"
        @completed="handleCompleted"
      />
    </Transition>
    <Transition name="bounce">
      <Intro :value="question.intro" v-if="introVisible" @close="handleIntroClose" />
    </Transition>
  </div>
</template>
<style scoped>
.scroll {
  border: 1px solid black;
  height: 30vh;
  margin-right: 25%;
  cursor: pointer;
  background: white;
  aspect-ratio: 5/7;
}

.scroll div {
  width: 80%;
  border: 1px solid rgb(61, 56, 56);
  margin-top: 6%;
  margin-bottom: 10%;
}
</style>
