<template>
  <div v-show="toggleInfo" class="full-screan-popup" @click="closeSideBar()"></div>
  <nav :class="toggleInfo ? 'show' : 'hide'">
    <Switch :switchBtn="switchMenu" @updateSwitchBtn="updateSwitchBtn"></Switch>
    <UnorderedList v-if="switchMenu" :navArr="navArr" :switchMenu="switchMenu"></UnorderedList>
    <UnorderedList v-else :navArr="navArr" :switchMenu="switchMenu"></UnorderedList>
  </nav>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Switch from "@/components/ui/Switch.vue";
import UnorderedList from "@/components/header/UnorderedList.vue";

onMounted(async () => {
  getNavInfos();
});

const navArr = ref(null);

function getNavInfos() {
  fetch("src/utils/data.json")
    .then(function (response) {
      return response.json();
    })
    .then(function (msg) {
      navArr.value = msg;
    });
}

function closeSideBar() {
  emit("updateToggle", false);
}

const updateSwitchBtn = (newValue) => {
  switchMenu.value = newValue;
};

const emit = defineEmits(["updateToggle"]);

const switchMenu = ref(false);

const props = defineProps({
  toggleInfo: {
    type: Boolean,
  },
});
</script>
<style lang="scss" scoped>
.full-screan-popup {
  position: absolute;
  width: 100vw;
  height: 100vh;
  top: 0;
  right: 0;
}
nav {
  padding: 10px 5px 20px;
  height: 100vh;
  width: 180px;
  background-color: #000000;
  position: absolute;
  top: 0;
  right: 0;
  z-index: 100;
  transition: transform 0.5s;
  overflow-y: scroll;
}

.hide {
  transform: translate(100%);
}

.show {
  transform: translate(0);
}
</style>
