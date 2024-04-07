<template>
  <div class="square" :class="addFlash ? 'flash' : ''"></div>
</template>
<script setup>
import { computed, onMounted } from "vue";

onMounted(() => {
  emit("updateSquareWidth", squareWidth.value);
});

const emit = defineEmits(["updateSquareWidth"]);

const squareWidth = computed(() => {
  return document.getElementsByClassName("square").item(0).getBoundingClientRect().width;
});

const addFlash = computed(() => {
  if (props.indexOfSpuare === 3 || props.indexOfSpuare === 5 || props.indexOfSpuare === 9) {
    return true;
  } else {
    return false;
  }
});

const props = defineProps({
  indexOfSpuare: {
    type: Number,
  },
});
</script>
<style lang="scss" scoped>
@keyframes flash {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 0.6;
  }
}
.square {
  width: 30%;
  height: 100px;
  border: black solid 2px;
  background: radial-gradient(circle, rgba(113, 81, 95, 1) 81%, rgba(0, 0, 0, 1) 100%);
  margin: 2px;
}

.flash {
  animation: flash 0.7s linear infinite;
}
</style>
