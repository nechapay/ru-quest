<script setup></script>
<template>
  <div class="table fill">
    <div class="book"></div>
    <div class="tablet"></div>
  </div>
</template>
<style scoped>
.table {
  display: flex;
  align-items: center;
  justify-content: center;
  border: 3px solid black;
  cursor: pointer;
}

.table:hover {
  border-color: #afa;
}

.book {
  width: 15%;
  height: 45%;
  border: 1px solid black;
  margin-right: 25%;
}

.tablet {
  background-image: url('/img/tablet.png');
  background-repeat: no-repeat;
  background-size: cover;
  width: 15%;
  height: 47%;
}
</style>
