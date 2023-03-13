<script setup>
import SVGLogo from "./SVGLogo.vue"
</script>

<template lang="pug">
.title.cursor-hover-item.big
  SVGLogo
  //- img.logo(src="../assets/Logo.jfif", alt="")
</template>

<style lang="stylus" scoped>
.title
  pos()
  flex()
  transform translate(-50%,-50%)
  color colorPrimary
  font-size 10rem
  line-height 10rem
  text-align center
  text-shadow 4px 4px 12px color_black
  // size()
// .logo
//   position absolute
//   left 50%
//   top 50%
//   transform translate(-50%,-50%)
//   mix-blend-mode difference
</style>
