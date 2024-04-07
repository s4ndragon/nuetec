<template>
  <li :class="showIt ? 'highlight' : null" @click.stop="clickText(navArrItem.key)" :key="navArrItem.key">
    {{ navArrItem.text }}
    <UnorderedList
      v-if="showChildren && navArrItem.children"
      :navArr="navArrItem.children"
      :switchMenu="switchMenu"></UnorderedList>
  </li>
</template>
<script setup>
import { ref, inject, onBeforeUnmount, computed, onMounted } from "vue";
import UnorderedList from "@/components/header/UnorderedList.vue";
const emitter = inject("emitter");

const theHighlightKey = ref(null);

onMounted(() => {
  emitter.on("highlightKey", (value) => {
    theHighlightKey.value = value;
  });
});

onBeforeUnmount(() => {
  emitter.off("highlightKey");
});

const showChildren = computed(() => {
  if (props.switchMenu) {
    return true;
  } else {
    if (props.navArrItem) {
      if (props.navArrItem.key === props.currentHighLightList) {
        return true;
      } else {
        return false;
      }
    } else {
      return false;
    }
  }
});

const showIt = computed(() => {
  if (props.switchMenu) {
    if (props.navArrItem) {
      if (props.navArrItem.key === props.currentHighLightList && theHighlightKey.value === props.navArrItem.key) {
        return true;
      } else {
        return false;
      }
    } else {
      return false;
    }
  } else {
    if (props.navArrItem) {
      if (props.navArrItem.key === props.currentHighLightList) {
        return true;
      } else {
        return false;
      }
    } else {
      return false;
    }
  }
});

function clickText(key) {
  emitter.emit("highlightKey", key);
  emit("sendListKey", key);
}

const emit = defineEmits(["sendListKey"]);
const props = defineProps({
  navArrItem: {
    type: Object,
  },
  currentHighLightList: {
    type: String,
  },
  switchMenu: {
    type: Boolean,
  },
});
</script>
<style lang="scss" scoped>
li {
  color: #b5b5b5;
  text-align: start;
  list-style: none;
  padding: 0px 0 5px 5px;
  padding: 10px 0 5px 5px;

  cursor: pointer;
}

.highlight {
  background-color: #828282;
  color: #f6ff7e;
}

.hightlight-bg {
}
</style>
