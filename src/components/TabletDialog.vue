<script setup>
const emits = defineEmits(['close'])
const props = defineProps(['tablet'])
function handleCloseClick() {
  emits('close')
}

function handleAuthorClick(evt, val) {
  let author = document.getElementById('auth_' + evt.target.id.split('_')[1])
  if (val) author.classList.add('correct')
  else author.classList.add('incorrect')
}
</script>

<template>
  <div class="dialog-wrapper fill base-flex" @click.self="handleCloseClick">
    <div class="dialog-body big-tablet base-flex flex-column">
      <div class="tablet-inner-wrapper">
        <div
          class="author-wrapper"
          v-for="item in tablet.authors"
          @click="handleAuthorClick($event, item.correct)"
          :id="`auth_${item.id}`"
        >
          <img :src="`./img/${item.img}`" :id="`img_${item.id}`" />
        </div>
      </div>
      <button class="tablet-close-button" @click="handleCloseClick" title="Закрыть"></button>
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
  width: 38%;
  height: 95%;
  padding: 2%;
  font-size: 1.2em;
  text-align: justify;
}

.big-tablet {
  background-image: url('/img/tablet.png');
  background-repeat: no-repeat;
  background-size: cover;
  width: 37.1%;
  /* height: 47%; */
  min-height: 240px;
  min-width: 172px;
}

.tablet-inner-wrapper {
  display: flex;
  flex-wrap: wrap;
  overflow-y: scroll;
  overflow-x: hidden;
  border: 1px solid black;
  width: 98%;
  height: 89%;
  margin-top: 8%;
  padding: 2%;
}

.tablet-inner-wrapper::-webkit-scrollbar {
  width: 10px;
}

.tablet-inner-wrapper::-webkit-scrollbar-track {
  background-color: #5c5a5a3f;
  border-radius: 100px;
}

.tablet-inner-wrapper::-webkit-scrollbar-thumb {
  background-color: rgb(151, 148, 148);
  border-radius: 100px;
}

.tablet-close-button {
  padding: 4%;
  border-radius: 50%;
  border: 4px solid #362727;
  position: relative;
  top: 3%;
  background: white;
  cursor: pointer;
}

.author-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  max-width: 25%;
  height: auto;
  padding: 1%;
  margin: 2%;
  cursor: pointer;
}

.author-wrapper.correct {
  background: rgb(3, 199, 3);
}

.author-wrapper.incorrect {
  background: rgb(247, 89, 89);
}

.author-wrapper img {
  max-width: 100%;
}
</style>
