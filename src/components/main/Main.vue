<template>
  <main>
    <Switch :switchBtn="direction" @updateSwitchBtn="updateSwitchBtn"></Switch>
    <div class="bingo">
      <Square v-for="n in numberOfSquares" :indexOfSpuare="n" @updateSquareWidth="updateSquareWidth"></Square>
      <Ball v-for="n in numberOfBalls" :indexOfBall="n" :squareWidth="squareWidth" :direction="direction"></Ball>
    </div>
  </main>
</template>
<script setup>
import { ref } from "vue";
import Switch from "@/components/ui/Switch.vue";
import Square from "@/components/main/Square.vue";
import Ball from "@/components/main/Ball.vue";

const numberOfSquares = ref(9);
const numberOfBalls = ref(5);

const direction = ref(false);
const updateSwitchBtn = (newValue) => {
  direction.value = newValue;
};

const squareWidth = ref(null);
const updateSquareWidth = (value) => {
  squareWidth.value = value;
};
</script>
<style lang="scss" scoped>
main {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: rgb(187, 187, 187);
  overflow: hidden;
  .bingo {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    position: relative;
  }
}
</style>
