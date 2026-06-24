<script setup>
import { computed, ref } from 'vue'
import viteLogo from '../assets/vite.svg'
import heroImg from '../assets/hero.png'
import vueLogo from '../assets/vue.svg'

const newItem = ref("")
const AddItem = ref(false)
const newItemHighPriority = ref(false)

const itemList = ref([
    { id: 1, label: "Item1", purchased: true, highPriority: false },
  { id: 2, label: "Item2", purchased: false, highPriority: false },
  { id: 3, label: "Item3", purchased: false, highPriority: true }
])
const saveItem = () => {
  itemList.value.push({ id: itemList.value.length + 1, label: newItem.value, highPriority: newItemHighPriority.value})
  newItem.value = ''
  newItemHighPriority.value = ''
}
const doEdit = (val) => {
  AddItem.value = val
  newItem.value = ''
  // itemList.value = []
}
const strikeItem = (item) => {
  item.purchased = !item.purchased
}
const reverseItems = computed(() => {
return [...itemList.value].reverse()
})

</script>

<template>
  <div>
    <h1>Shopping Time</h1>
    <!-- v-on:click -->
    <button @click="doEdit(false)" v-if="AddItem">Cancel</button>
    <button @click="doEdit(true)" v-else>Add Item</button>
  </div>
  <br />
   <!-- use @keydown.enter.prevent to prevent enter action -->
  <form 
  @submit.prevent=" saveItem"
  v-if="AddItem"
  >
    <input type="text" placeholder="Enter item names" v-model="newItem">
    <label>
      <input type="checkbox" v-model="newItemHighPriority">
      High Priority
    </label>
    <br />
    <p>{{ newItem }}</p>
    <!-- v-bind:disabled -->
    <button :disabled="!newItem.length" >Save Item</button> 
  </form>
  <ul>
    <li 
    :key="index" v-for="(item, index) in reverseItems"
    :class="{strikeout : item.purchased, highlight : item.highPriority}" 
    @click="strikeItem(item)"
    >
    {{ item.label }}
    </li>
  </ul>
  <p v-if="!itemList.length">
    All Caught Out !!!
  </p>
</template>

<style src="./ShoppingListStyle.css"></style>
