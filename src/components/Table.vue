<script setup>
import { ref } from 'vue'
import TabletDialog from './TabletDialog.vue'
import ScrollDialog from './ScrollDialog.vue'

const props = defineProps(['question'])

let tabletDialogVisible = ref(false)
let scrollDialogVisible = ref(false)

function handleScrollClose() {
  scrollDialogVisible.value = false
}
</script>
<template>
  <div class="table fill">
    <div class="book" @click="scrollDialogVisible = true"></div>
    <div class="tablet"></div>
  </div>
  <Transition name="bounce">
    <ScrollDialog v-if="scrollDialogVisible" @close="handleScrollClose" :scroll="question?.scroll"/>
  </Transition>
  <Transition name="bounce">
    <TabletDialog v-if="tabletDialogVisible" :tablet="question?.tablet"/>
  </Transition>
</template>
<style scoped>
.table {
  display: flex;
  align-items: center;
  justify-content: center;
  border: 3px solid black;
}

.book {
  width: 15%;
  height: 45%;
  border: 1px solid black;
  margin-right: 25%;
  min-height: 240px;
  min-width: 172px;
  cursor: pointer;
}

.tablet {
  background-image: url('/img/tablet.png');
  background-repeat: no-repeat;
  background-size: cover;
  width: 15%;
  /* height: 47%; */
  min-height: 240px;
  min-width: 172px;
  cursor: pointer;
}
</style>
