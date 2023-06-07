<script setup>
const props = defineProps(['letters', 'finished'])
const emits = defineEmits(['finished'])

function handleLetterClick(evt) {
  if (evt.target.value == props.letters.correct) {
    evt.target.classList.add('correct')
    emits('finished')
  } else evt.target.classList.add('incorrect')
}
</script>
<template>
  <div class="tablet-inner-wrapper justify-center">
    <span>{{ letters.title }}</span>
    <div class="message-container base-flex">
      <Transition name="fade">
        <span v-if="finished" v-html="letters.message"></span>
      </Transition>
    </div>
    <div class="letters-wrapper base-flex">
      <button class="alpha-letter" v-for="item in letters.list.split('')" :value="item" @click="handleLetterClick">
        {{ item }}
      </button>
    </div>
  </div>
</template>

<style lang="css" scoped>
.alpha-letter {
  font-size: 2rem;
  background: white;
  border: 1px solid green;
  transition-duration: 0.3s;
  padding: 2% 4%;
  min-width: 18%;
  margin: 0.5%;
  cursor: pointer;
  font-weight: bold;
}

.alpha-letter.correct {
  color: rgb(3, 199, 3);
  cursor: auto;
}

.alpha-letter.incorrect {
  color: rgb(247, 89, 89);
  border: 1px solid rgb(247, 89, 89);
  cursor: auto;
  animation: tilt-shaking 0.15s;
}

.alpha-letter:hover {
  background: green;
  color: white;
}

.letters-wrapper {
  width: 100%;
  flex-wrap: wrap;
}

.message-container {
  width: 100%;
  height: 30%;
}
</style>
