<script setup>
const emits = defineEmits(['close'])
function handleCloseClick() {
  emits('close')
}
</script>

<template>
  <div class="dialog-wrapper fill base-flex">
    <div class="dialog-body"></div>
    <button @click="handleCloseClick">Close</button>
  </div>
</template>

<style lang="css" scoped>
.dialog-wrapper {
  z-index: 2;
  position: fixed;
  top: 0;
  left: 0;
}

.dialog-body {
  background: white;
  width: 90%;
  height: 60%;
}
</style>
