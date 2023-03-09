<script setup>
import { ref } from "vue"
import { RouterLink, RouterView } from "vue-router"
import { NButton, NDropdown, useMessage } from "naive-ui"
import Menu from "./components/Menu.vue"
import Cursor from "./components/Cursor.vue"
import Title from "./components/Title.vue"

// const message = useMessage()
const showDropdownRef = ref(false)

const options = ref([
  {
    label: "Marina Bay Sands",
    key: "Marina Bay Sands",
    disabled: true,
  },
  {
    label: "Brown's Hotel, London",
    key: "Brown's Hotel, London",
  },
  {
    label: "Atlantis Bahamas, Nassau",
    key: "Atlantis Bahamas, Nassau",
  },
  {
    label: "The Beverly Hills Hotel, Los Angeles",
    key: "The Beverly Hills Hotel, Los Angeles",
  },
])

const handleSelect = (key) => {
  // message.info(String(key))
}
const handleClick = () => {
  showDropdownRef.value = !showDropdownRef.value
}
</script>

<template lang="pug">
//- n-message-provider
//-   n-dropdown( trigger="hover" :options="options" @select="handleSelect")
//-     n-button Hover!
Cursor
Menu
Title
//- RouterView
</template>

<style lang="stylus" scoped></style>
