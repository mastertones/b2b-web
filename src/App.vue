<script setup>
import { ref } from "vue"
import { RouterLink, RouterView } from "vue-router"
import { NConfigProvider } from "naive-ui"
import Menu from "./components/Menu.vue"
import Cursor from "./components/Cursor.vue"
import Title from "./components/Title.vue"

// const message = useMessage()

const color_yellow = "#e3ff7b"
const color_brown = "#D4C8BE"
const color_green = "#00dcb4"
const color_grey = "#f4f5f7"
const color_blue = "#3a99ff"
const color_purple = "#ac94fa"
const color_black = "#262622"
const color_red = "#f98080"

const themeOverrides = {
  common: {
    primaryColor: color_blue,
    hoverColor: color_blue,
  },
  Menu: {
    itemTextColorHoverHorizontal: color_blue,
    itemTextColorChildHover: color_grey,
    fontSize: "1rem",
    itemHeight: "60px",
  },
}
</script>

<template lang="pug">
n-config-provider(:theme-overrides='themeOverrides' )
  Cursor
  Menu
  Title
//- RouterView
</template>

<style lang="stylus" scoped></style>
