<template>
  <div :style="{ height: totalHeight + 'px'}">
    <div :style="{transform: 'translateY(' + scrollTop + 'px)'}">
      <Item v-for="item in validItems" :item="item" :key="item.id" />
    </div>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from "vue";
import Item from "./ItemList.vue";
const dataLength = 100;
let items = [];
for (let i = 1; i <= dataLength; i++) {
  items.push({
    id: i,
    name: "item" + i,
  });
}

const maxHeight = window.innerHeight - 60 - 40;
const rowHeight = 44;
const totalHeight = ref(dataLength * rowHeight);
const start = ref(0);
const end = ref(Math.ceil(maxHeight / rowHeight));
const validItems = ref(items.slice(start.value, end.value));
const scrollTop = ref(0);
const buffer = 10; // 滚动缓冲区

function handleWheel(event) {
  // 在鼠标滚轮事件中，event.deltaY 表示垂直方向的滚动距离，event.deltaX 表示水平方向的滚动距离
  const scrollDirection = event.deltaY > 0 ?  1 : -1;
  const scrollItems = Math.abs(Math.floor(event.deltaY / rowHeight)); // 计算滚动的项数
  start.value = Math.max(0, start.value + scrollDirection * scrollItems); // 更新起始位置
  end.value = start.value + Math.ceil(maxHeight / rowHeight); // 更新结束位置
  console.log(start.value, end.value);
  validItems.value = items.slice(start.value, end.value + buffer); // 更新可见项
  scrollTop.value = -start.value * rowHeight; // 更新滚动位置
  if (start.value === 0 || end.value === dataLength) {
    event.preventDefault(); // 阻止默认滚动行为
  }
}

onMounted(() => {
  window.addEventListener("wheel", (e) => handleWheel(e));
});

onUnmounted(() => {
  window.removeEventListener("wheel", (e) => handleWheel(e));
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
