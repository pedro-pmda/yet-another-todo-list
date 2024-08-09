<script setup lang="ts">
import ListItem from '@/components/ListItem.vue'
import { computed, onMounted, ref, type Ref } from 'vue'

interface Item {
  title: string
  checked: boolean
}

const storageItems: Ref<Item[]> = ref([])

const initListItems = (): void => {
  if (storageItems.value?.length === 0) {
    const listItems: Item[] = [
      { title: 'Clean the kitchen', checked: false },
      { title: 'Do the laundry', checked: false },
      { title: 'Vacuum the living room', checked: false },
      { title: 'Water the plants', checked: false },
      { title: 'Organize the closet', checked: false },
      { title: 'Take out the trash', checked: false },
      { title: 'Mow the lawn', checked: false },
      { title: 'Wash the dishes', checked: false },
      { title: 'Prepare meals for the week', checked: false },
      { title: 'Change bed sheets', checked: false }
    ]
    setToStorage(listItems)
    storageItems.value = listItems
  }
}

onMounted(() => {
  initListItems()
  storageItems.value = getFromStorage()
})

const updateItem = (item: Item): void => {
  const updateItem = findItemInList(item)
  if (updateItem) {
    toggleItemChecked(updateItem)
    setToStorage(storageItems.value)
  }
}

const findItemInList = (item: Item): Item | undefined => {
  return storageItems.value.find((itemList: Item) => itemList.title === item.title)
}

const toggleItemChecked = (item: Item): void => {
  item.checked = !item.checked
}

const sortList = computed(() =>
  [...storageItems.value].sort((a, b) => (a.checked ? 1 : 0) - (b.checked ? 1 : 0))
)

const KEY_LIST_ITEMS_STORAGE = 'list-items'

const setToStorage = (items: Item[]): void => {
  localStorage.setItem(KEY_LIST_ITEMS_STORAGE, JSON.stringify(items))
}

const getFromStorage = (): Item[] => {
  const stored = localStorage.getItem(KEY_LIST_ITEMS_STORAGE)
  if (stored) {
    return JSON.parse(stored)
  } else {
    return []
  }
}
</script>

<template>
  <ul>
    <li :key v-for="(item, key) in storageItems">
      <ListItem :is-checked="item.checked" @click.prevent="updateItem(item)">
        {{ item.title }}
      </ListItem>
    </li>
  </ul>
</template>

<style scoped>
ul {
  list-style: none;
}

li {
  margin: 0.4rem 0;
}
</style>
