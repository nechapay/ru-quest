<script setup>
const emits = defineEmits(['close'])
const props = defineProps(['value'])
function handleCloseClick() {
  emits('close')
}
</script>

<template>
  <div class="dialog-wrapper fill base-flex" @click.self="handleCloseClick">
    <div class="dialog-body base-flex flex-column">
      <span v-html="value.text"></span>
      <br />
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
  width: 65%;
  border: 1px solid black;
  padding: 2%;
  font-size: 200%;
  text-align: justify;
  aspect-ratio: 16/9;
}

li {
  margin-bottom: 1em;
}
</style>
