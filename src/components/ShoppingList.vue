<script setup>
import { ref } from 'vue'
import viteLogo from '../assets/vite.svg'
import heroImg from '../assets/hero.png'
import vueLogo from '../assets/vue.svg'

const itemList = ref([{ id: 1, label: "Item1" },
{ id: 2, label: "Item2" },
{ id: 3, label: "Item3" }])
const newItem = ref("")
const saveItem = () => {
  itemList.value.push({ id: itemList.value.length + 1, label: newItem.value })
  newItem.value = ''
}
</script>

<template>
  <h1>Shopping Time</h1>
    <form @submit.prevent="saveItem"> <!-- use @keydown.enter.prevent to prevent enter action -->
    <input type="text" placeholder="Enter item names" v-model="newItem" />

    <button>Drop</button>
    <br />
    <p>{{ newItem }}</p>
  </form>
  <ol>
    <li :key="index" v-for="({ id, label }, index) in itemList">{{ label }}</li>
  </ol>
</template>
