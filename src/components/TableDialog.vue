<script setup>
import Table from './Table.vue'
</script>

<template>
  <div class="dialog-wrapper fill base-flex">
    <div class="dialog-body">
      <Table />
    </div>
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
