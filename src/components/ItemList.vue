<script setup lang="ts">
import { ref } from 'vue'

interface Item {
  name: string
}
interface Item2 {
  name: string,
  limit: string
}

const mikan_items = ref<Item2[]>([
  { name: 'なろう' ,limit: '明日'},
  { name:'なろう２', limit:'一週間後'}
])

const done_items = ref<Item[]>([
  { name: '仏縁レポート'}
])
const newItemName = ref('')
const newItemLimit = ref('')

const addItem = () => {
  if (newItemName.value) {
    mikan_items.value.push({ name: newItemName.value,limit:newItemLimit.value})
    newItemName.value = ''
  }
}

const changeState = (item: Item2) => {
  const index = mikan_items.value.indexOf(item);
  if (index !== -1) {
    const removedItem = mikan_items.value.splice(index, 1)[0];
    done_items.value.push(removedItem);
  }
}

const deleteItem = (item: Item) => {
  const index = done_items.value.indexOf(item);
  if (index !== -1) {
    done_items.value.splice(index, 1)[0];
  }
}
</script>

<template>
    <div>
      <div>やるべきタスク</div>
      <ul>
        <li v-for="mikanitem in mikan_items" :key="mikanitem.name">
          <div>タスク: {{( mikanitem.name )}}</div>
          <div>タスク: {{( mikanitem.limit )}}</div>
          <button @click="() => changeState(mikanitem)">終わった！</button>
        </li>
    </ul>
    <div>成し遂げたタスク</div>
    <ul>
        <li v-for="doneitem in done_items" :key="doneitem.name">
          <div>タスク: {{ doneitem.name }}</div>
          <button @click="() => deleteItem(doneitem)">削除する</button>
        </li>
      </ul>
      <div>
        <label>
          タスク名
          <input v-model="newItemName" type="text" />
        </label>
        <label>
          期限
          <input v-model="newItemLimit" type="text" />
        </label>
        <button @click="addItem">add</button>
      </div>
    </div>
  </template>

  <style>
  </style>