<template>
  <div class="container" :class="toggleInfo ? 'open' : ''">
    <div class="bar bar1"></div>
    <div class="bar bar2"></div>
    <div class="bar bar3"></div>
  </div>
</template>
<script setup>
const props = defineProps({
  toggleInfo: {
    type: Boolean,
  },
});
</script>
<style lang="scss" scoped>
.container {
  display: inline-block;
  cursor: pointer;
  padding: 0 20px;
  .bar {
    width: 35px;
    height: 5px;
    background-color: #333;
    margin: 6px 0;
    transition: 0.4s;
  }
}

.open {
  .bar1 {
    transform: translate(0, 11px) rotate(-45deg);
  }
  .bar2 {
    opacity: 0;
  }
  .bar3 {
    transform: translate(0, -11px) rotate(45deg);
  }
}
</style>
