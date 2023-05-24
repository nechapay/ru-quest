<script setup>
import { computed, ref } from 'vue'
import TabletDialog from './TabletDialog.vue'
import ScrollDialog from './ScrollDialog.vue'

const props = defineProps(['question'])
const emits = defineEmits(['finished'])
let faded = ref(false)

let tabletDialogVisible = ref(false)
let scrollDialogVisible = ref(false)

const tabletVisible = computed(() => !tabletDialogVisible.value)

function showDialog(dialog, val) {
  if (!dialog) return
  if (dialog === 'tablet') tabletDialogVisible.value = val
  if (dialog === 'scroll') scrollDialogVisible.value = val
  faded.value = val
}
</script>
<template>
  <div class="table fill">
    <Transition name="bounce">
      <div class="book" @click="showDialog('scroll', true)"></div>
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
      />
    </Transition>
  </div>
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

/* .tablet {
  background-image: url('/img/tablet.png');
  background-repeat: no-repeat;
  background-size: cover;
  width: 15%;
  height: 47%; 
  min-height: 240px;
  min-width: 172px;
  cursor: pointer;
} */

.transparent-fader {
  position: fixed;
  top: 0;
  left: 0;
  background: rgba(128, 128, 128, 0.425);
}
</style>
