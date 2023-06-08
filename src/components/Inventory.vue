<script setup>
import { ref } from 'vue'
import draggable from 'vuedraggable'
const props = defineProps(['inventory', 'enabled'])
let dragging = ref(false)
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
        {{ element.name }}
      </div>
    </template>
  </draggable>
</template>

<style lang="css" scoped></style>
