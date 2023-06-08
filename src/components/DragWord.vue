<script setup>
import { computed, ref, watch } from 'vue'
import draggable from 'vuedraggable'

const props = defineProps(['correct'])
const emits = defineEmits(['completed'])

const enabled = ref(true)

const list1 = ref([
  {
    id: 1,
    name: 'А'
  },
  {
    id: 2,
    name: 'Б'
  },
  {
    id: 3,
    name: 'В'
  },
  {
    id: 4,
    name: 'Г'
  },
  {
    id: 5,
    name: 'Д'
  },
  {
    id: 6,
    name: 'Е'
  },
  {
    id: 7,
    name: 'Ё'
  },
  {
    id: 8,
    name: 'Ж'
  },
  {
    id: 9,
    name: 'З'
  },
  {
    id: 10,
    name: 'И'
  },
  {
    id: 11,
    name: 'Й'
  },
  {
    id: 12,
    name: 'К'
  },
  {
    id: 13,
    name: 'Л'
  },
  {
    id: 14,
    name: 'М'
  },
  {
    id: 15,
    name: 'Н'
  },
  {
    id: 16,
    name: 'О'
  },
  {
    id: 17,
    name: 'П'
  },
  {
    id: 18,
    name: 'Р'
  },
  {
    id: 19,
    name: 'С'
  },
  {
    id: 20,
    name: 'Т'
  },
  {
    id: 21,
    name: 'У'
  },
  {
    id: 22,
    name: 'Ф'
  },
  {
    id: 23,
    name: 'Х'
  },
  {
    id: 24,
    name: 'Ц'
  },
  {
    id: 25,
    name: 'Ч'
  },
  {
    id: 26,
    name: 'Ш'
  },
  {
    id: 27,
    name: 'Щ'
  },
  {
    id: 28,
    name: 'Ъ'
  },
  {
    id: 29,
    name: 'Ы'
  },
  {
    id: 30,
    name: 'Ь'
  },
  {
    id: 31,
    name: 'Э'
  },
  {
    id: 32,
    name: 'Ю'
  },
  {
    id: 33,
    name: 'Я'
  }
])

const word = ref([])

let answer = computed(() => word.value.map((i) => i.name).join(''))

watch(answer, (newValue, oldValue) => {
  if (newValue === props.correct) {
    enabled.value = false
    emits('completed')
  }
})
</script>

<template>
  <div class="drag-word-wrapper base-flex flex-column">
    <draggable
      :list="word"
      :disabled="!enabled"
      item-key="id"
      group="people"
      class="list-group word-wrapper base-flex"
      ghost-class="ghost"
      @change="word.splice(7)"
      @start="dragging = true"
      @end="dragging = false"
    >
      <template #item="{ element }">
        <div class="list-group-item letter base-flex" :class="{ 'not-draggable': !enabled }">
          {{ element.name }}
        </div>
      </template>
    </draggable>
    <draggable
      :list="list1"
      :disabled="!enabled"
      item-key="id"
      :group="{ name: 'people', pull: 'clone', put: false }"
      class="list-group base-flex flex-wrap"
      ghost-class="ghost"
      @start="dragging = true"
      @end="dragging = false"
    >
      <template #item="{ element }">
        <div class="list-group-item letter letter--small base-flex" :class="{ 'not-draggable': !enabled }">
          {{ element.name }}
        </div>
      </template>
    </draggable>
  </div>
</template>

<style lang="css" scoped>
.drag-word-wrapper {
  margin-top: auto;
  height: 35%;
}

.letter--small {
  width: 35px;
  height: 35px;
  background: white;
  color: black;
  font-size: 1.2rem;
  text-shadow: none;
}

.word-wrapper {
  width: 88%;
  height: 20%;
  border: 1px solid rgb(94, 88, 88);
  min-height: 106px;
  background: rgba(94, 88, 88, 0.4);
}
</style>
