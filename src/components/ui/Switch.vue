<template>
  <label class="switch">
    <input type="checkbox" v-model="switchValue" />
    <span class="slider"></span>
  </label>
</template>
<script setup>
import { computed } from "vue";

const switchValue = computed({
  get() {
    return props.switchBtn;
  },
  set(newValue) {
    emit("updateSwitchBtn", newValue);
  },
});

const emit = defineEmits(["updateSwitchBtn"]);

const props = defineProps({
  switchBtn: {
    type: Boolean,
  },
});
</script>
<style lang="scss" scoped>
.switch {
  position: relative;
  display: inline-block;
  width: 46px;
  height: 30px;
  margin-left: 10px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #828282;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 20px;
  width: 20px;
  left: 4px;
  bottom: 4px;
  background-color: #ccc;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

input:checked + .slider {
  background-color: rgb(34, 34, 218);
}

input:focus + .slider {
  box-shadow: 0 0 1px rgb(34, 34, 218);
}

input:checked + .slider:before {
  -webkit-transform: translateX(20px);
  -ms-transform: translateX(20px);
  transform: translateX(18px);
}
</style>
