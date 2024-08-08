<script setup lang="ts">
import ListItem from '@/components/ListItem.vue'

interface Item {
  title: string
  checked: boolean
}

const listItems: Item[] = [
  { title: 'Clean the kitchen', checked: true },
  { title: 'Do the laundry', checked: false },
  { title: 'Vacuum the living room', checked: false },
  { title: 'Water the plants', checked: true },
  { title: 'Organize the closet', checked: false },
  { title: 'Take out the trash', checked: true },
  { title: 'Mow the lawn', checked: false },
  { title: 'Wash the dishes', checked: false },
  { title: 'Prepare meals for the week', checked: false },
  { title: 'Change bed sheets', checked: true }
]
</script>

<template>
  <ul>
    <li :key v-for="(item, key) in listItems">
      <ListItem :is-checked="false">{{ item.title }}</ListItem>
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
