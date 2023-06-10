<script setup lang="ts">
import { ref } from 'vue'

interface Item {
  name: string
}

const mikan_items = ref<Item[]>([
  { name: 'なろう'},
  { name:'なろう２'}
])

const done_items = ref<Item[]>([
  { name: '仏縁レポート'}
])
const newItemName = ref('')

const addItem = () => {
  if (newItemName.value) {
    mikan_items.value.push({ name: newItemName.value})
    newItemName.value = ''
  }
}

const changeState = (item: Item) => {
  const index = mikan_items.value.indexOf(item);
  if (index !== -1) {
    const removedItem = mikan_items.value.splice(index, 1)[0];
    done_items.value.push(removedItem);
  }
}
</script>

<template>
    <div>
      <div>やるべきタスク</div>
      <ul>
        <li v-for="mikanitem in mikan_items" :key="mikanitem.name">
          <div>タスク: {{( mikanitem.name )}}</div>
          <button @click="() => changeState(mikanitem)">終わった！</button>
        </li>
    </ul>
    <div>成し遂げたタスク</div>
    <ul>
        <li v-for="doneitem in done_items" :key="doneitem.name">
          <div>タスク: {{ doneitem.name }}</div>
        </li>
      </ul>
      <div>
        <label>
          名前
          <input v-model="newItemName" type="text" />
        </label>
        <button @click="addItem">add</button>
      </div>
    </div>
  </template>
  
  <style>
  </style>