<template>
  <header>
    <MenuIcon @click="toggleOpen()" :toggleInfo="openOrNot"></MenuIcon>
    <NavBar :toggleInfo="openOrNot" @updateToggle="updateToggle"></NavBar>
  </header>
</template>
<script setup>
import { ref } from "vue";
import MenuIcon from "@/components/header/MenuIcon.vue";
import NavBar from "@/components/header/NavBar.vue";
const openOrNot = ref(false);

function toggleOpen() {
  openOrNot.value = !openOrNot.value;
}

const updateToggle = (value) => {
  openOrNot.value = value;
};
</script>
<style lang="scss" scoped>
header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 60px;
  z-index: 5;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  background-color: #fff;
}
</style>
