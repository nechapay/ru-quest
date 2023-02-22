<script setup>
import TheCanvas from './TheCanvas.vue'
import { useElementSize } from '@vueuse/core'
import { onMounted, ref } from 'vue'

const mainPage = ref()

const elementSize = useElementSize(mainPage)
let size = {
  width: 0,
  height: 0
}
onMounted(() => {  
  size.width = elementSize.width.value
  size.height = elementSize.height.value
  console.log(elementSize.width.value, elementSize.height.value)
})
</script>
<template>
  <div class="main-page-container" ref="mainPage">
    <TheCanvas :someSize="size" />
  </div>
</template>

<style scoped>
.main-page-container {
  width: 80%;
  height: 80%;
  margin: 5% 10%;
  border: 1px solid black;
}
</style>
