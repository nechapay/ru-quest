<script setup>
import _ from 'lodash'
const props = defineProps(['authors'])
const emits = defineEmits(['finished'])

function handleAuthorClick(evt, val) {
  let element = document.getElementById('auth_' + evt.target.id.split('_')[1])
  if (val.correct) {
    element.classList.add('correct')
    emits('finished')
  } else element.classList.add('incorrect')
}
</script>
<template>
  <div class="tablet-inner-wrapper">
    <div
      class="author-wrapper"
      v-for="item in _.shuffle(authors)"
      @click="handleAuthorClick($event, item)"
      :id="`auth_${item.id}`"
    >
      <img :src="`./img/${item.img}`" :id="`img_${item.id}`" />
      <span>{{ item.name }}</span>
    </div>
  </div>
</template>
<style lang="css" scoped>
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
  animation: tilt-shaking 0.15s;
}

.author-wrapper img {
  max-width: 100%;
  height: 95%;
}
</style>
