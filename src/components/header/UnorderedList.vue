<template>
  <ul>
    <List
      v-for="item in navArr"
      :navArrItem="item"
      :currentHighLightList="currentHighLightList"
      :key="item.key"
      @sendListKey="sendListKey"
      :switchMenu="switchMenu"></List>
  </ul>
</template>
<script setup>
import { ref } from "vue";
import List from "@/components/header/List.vue";

const currentHighLightList = ref("");

const sendListKey = (value) => {
  currentHighLightList.value = value;
};

const props = defineProps({
  navArr: {
    type: Array,
  },
  switchMenu: {
    type: Boolean,
  },
});
</script>
<style lang="scss" scoped>
ul {
  padding: 5px 5px 0px 5px;
}
</style>
