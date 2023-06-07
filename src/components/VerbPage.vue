<script setup>
const props = defineProps(['verb', 'finished'])
const emits = defineEmits(['finished'])

function handleLetterClick(evt, val) {
  if (val === ' ') return
  if (val.toLowerCase() === props.verb.correct.toLowerCase()) {
    evt.target.classList.add('correct')
    emits('finished')
  } else evt.target.classList.add('incorrect')
}
</script>
<template>
  <div class="tablet-inner-wrapper justify-center">
    <span>{{ verb.title }}</span>
    <div class="verb-wrapper base-flex">
      <span class="verb-letter blank">{{ verb.pre }}</span>
      <span
        class="verb-letter"
        :class="{ blank: item === ' ' }"
        @click="handleLetterClick($event, item)"
        v-for="item in verb.main.split('')"
        >{{ item }}</span
      >
      <span class="verb-letter blank">{{ verb.post }}</span>
    </div>
    <div class="message-container base-flex">
      <Transition name="fade">
        <span v-if="finished" v-html="verb.message"></span>
      </Transition>
    </div>
  </div>
</template>

<style lang="css" scoped>
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
  animation: tilt-shaking 0.15s;
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

.verb-wrapper {
  width: 100%;
  flex-wrap: wrap;
}

.message-container {
  width: 100%;
  height: 30%;
}
</style>
