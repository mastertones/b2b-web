<script setup>
import IconInstagram from "./icons/IconInstagram.vue"
import IconFacebook from "./icons/IconFacebook.vue"
import IconTwitter from "./icons/IconTwitter.vue"
</script>

<template lang="pug">
.contact
  a.cursor-hover-item(href="https://www.instagram.com/master_tones/" target="_blank") 
    IconInstagram
  a.cursor-hover-item(href="https://www.facebook.com/mastertones" target="_blank") 
    IconFacebook  
  a.cursor-hover-item(href="https://twitter.com/mastertonesltd" target="_blank") 
    IconTwitter  
</template>

<style lang="stylus" scoped>
.contact
  flex()
  size(auto)
  position absolute
  right 1rem
  bottom 1rem
  a
    flex()
    size(4rem)
    color color_black
    text-decoration none
</style>
