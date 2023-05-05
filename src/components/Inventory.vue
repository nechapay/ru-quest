<script setup>
import { ref } from 'vue'
import draggable from 'vuedraggable'
const props = defineProps(['inventory'])
let dragging = ref(false)
let enabled = ref(true)
</script>
<template>
  <draggable
    :list="inventory"
    :disabled="!enabled"
    item-key="id"
    class="list-group"
    ghost-class="ghost"
    @start="dragging = true"
    @end="dragging = false"
  >
    <template #item="{ element }">
      <div class="list-group-item letter base-flex" :class="{ 'not-draggable': !enabled }">
        {{ element.value }}
      </div>
    </template>
  </draggable>
</template>

<style lang="css" scoped>
.letter {
  width: 100px;
  height: 100px;
  border: 1px solid black;
  margin: 5px;
  background: linear-gradient(to bottom, #4096ee 0%, #4096ee 100%);
  user-select: none;
}
</style>
