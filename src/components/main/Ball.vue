<template>
  <div class="ball" :class="`ball-${indexOfBall}`">{{ position }}</div>
</template>
<script setup>
import { computed } from "vue";

const position = computed(() => {
  props.squareWidth;
  Array.from(document.getElementsByClassName(`ball-${props.indexOfBall}`)).forEach(
    (element) =>
      (element.style.transform = `translate(${
        props.indexOfBall % 4 === 0 || props.indexOfBall % 4 === 3
          ? `${props.squareWidth + 2 * 2}`
          : `-${props.squareWidth + 2 * 2}`
      }px, ${
        props.indexOfBall % 4 === 0 || props.indexOfBall % 4 === 1 ? `${(300 + 2 * 6) / 3}` : `-${(300 + 2 * 6) / 3}`
      }px`)
  );
  if (props.direction) {
    Array.from(document.getElementsByClassName(`ball-${props.indexOfBall}`)).forEach((element) =>
      element.animate(
        [
          {
            transform: `translate(${
              props.indexOfBall % 4 === 0 || props.indexOfBall % 4 === 3
                ? `${props.squareWidth + 2 * 2}`
                : `-${props.squareWidth + 2 * 2}`
            }px, ${
              props.indexOfBall % 4 === 0 || props.indexOfBall % 4 === 1
                ? `${(300 + 2 * 6) / 3}`
                : `-${(300 + 2 * 6) / 3}`
            }px)`,
          },
          {
            transform: `translate(0px, 0px)`,
            offset: 0.8,
          },
          {
            transform: `translate(0px, 0px)`,
          },
        ],
        { duration: 1000, iterations: Infinity }
      )
    );
  } else {
    Array.from(document.getElementsByClassName(`ball-${props.indexOfBall}`)).forEach((element) =>
      element.animate(
        [
          {
            transform: `translate(${
              props.indexOfBall % 4 === 0 || props.indexOfBall % 4 === 3
                ? `${props.squareWidth + 2 * 2}`
                : `-${props.squareWidth + 2 * 2}`
            }px, ${
              props.indexOfBall % 4 === 0 || props.indexOfBall % 4 === 1
                ? `${(300 + 2 * 6) / 3}`
                : `-${(300 + 2 * 6) / 3}`
            }px)`,
          },
          {
            transform: `translate(${
              props.indexOfBall % 4 === 0 || props.indexOfBall % 4 === 3
                ? `${props.squareWidth + 2 * 2 + (props.squareWidth + 2 * 2) * 2}`
                : `${props.squareWidth + 2 * 2}`
            }px, ${
              props.indexOfBall % 4 === 0 || props.indexOfBall % 4 === 1
                ? `${(300 + 2 * 6) / 3}`
                : `-${(300 + 2 * 6) / 3}`
            }px)`,
            offset: 0.8,
          },
          {
            transform: `translate(${
              props.indexOfBall % 4 === 0 || props.indexOfBall % 4 === 3
                ? `${props.squareWidth + 2 * 2 + (props.squareWidth + 2 * 2) * 2}`
                : `${props.squareWidth + 2 * 2}`
            }px, ${
              props.indexOfBall % 4 === 0 || props.indexOfBall % 4 === 1
                ? `${(300 + 2 * 6) / 3}`
                : `-${(300 + 2 * 6) / 3}`
            }px)`,
            // offset: 0.99,
          },
        ],
        { duration: 1000, iterations: Infinity }
      )
    );
  }

  return "0";
});

const props = defineProps({
  indexOfBall: {
    type: Number,
    default: 0,
  },
  squareWidth: {
    type: Number,
  },
  direction: {
    type: Boolean,
  },
});
</script>
<style lang="scss" scoped>
.ball {
  width: 30px;
  height: 30px;
  background-color: #a5f12b;
  border-radius: 50%;
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
