<script setup>
// import ToDoFooter from './components/ToDoFooter.vue';
// import ToDoList from './components/ToDoList.vue';
// import ToDoHeader from './components/ToDoHeader.vue';

import { computed, ref } from 'vue';

// 维护一个全局自增的计数ID
let defaultId = 0;

// 添加主界面
const items = ref([
  { id: defaultId ++, text: "do something1", done: false },
  { id: defaultId ++, text: "do something2", done: false },
  { id: defaultId ++, text: "do something3", done: false }
]);

// 获取输入框的值
const inputValue = ref('');

// 增加Item
function addItem(item) {
  items.value.push(item);
}

// 修改Item
function toggleItem(item) {
  items.value.forEach(curItem => {
    if (curItem.id === item.id) {
      item.done = !item.done;
    }
  })
}

// 删除Item
function removeItem(item) {
  items.value = items.value.filter(curItem => curItem.id !== item.id);
}

// 计数已完成的Item
const countDone = computed(() => {
  return items.value.filter(item => item.done).length;
})

// 计数总的Item
const countTotal = computed(() => {
  return items.value.length;
})
</script>

<template>
  <h1>这是一个待办事项</h1>
  <input type="text" v-model="inputValue" placeholder="add ToDo">
  <button @click = "addItem({id: defaultId ++, text: inputValue, done: false})">add</button>
  <ul>
    <li v-for="item in items" :key="item.id">
      <input type="checkbox" :checked="item.done" @change="toggleItem(item)">
      <span :class="{done: item.done}">{{ item.text }}</span>
      <button @click="removeItem(item)">delete</button>
    </li>
  </ul>
  <div>
    <span>已完成: {{ countDone }} / {{ countTotal }}</span>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
