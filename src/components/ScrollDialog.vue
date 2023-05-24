<script setup>
const emits = defineEmits(['close'])
const props = defineProps(['scroll'])
function handleCloseClick() {
  emits('close')
}
</script>

<template>
  <div class="dialog-wrapper fill base-flex" @click.self="handleCloseClick">
    <div class="dialog-body base-flex flex-column">
      <span v-html="scroll.text"></span>
      <br />
      <ul>
        <li v-for="item in scroll.list" v-html="item"></li>
      </ul>
      <button class="close-button" @click="handleCloseClick">Закрыть</button>
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
  background: white;
  height: 95%;
  border: 1px solid black;
  padding: 2%;
  font-size: 100%;
  text-align: justify;
  aspect-ratio: 5/7;
}

li {
  margin-bottom: 1em;
}
</style>
