<script setup>
import { gsap } from "gsap"
import { onMounted, ref } from "vue"
import { useMousePosition } from "../api"

const cursor = ref()
const cursorOuter = ref()
const cursorInner = ref()
const cursorTextContainerEl = ref()
const cursorTextEl = ref()

const hoverEffectDuration = ref(0.3)
let isHovered = ref(false)
let initialCursorHeight = ref()
const cursorRotationDuration = ref(8)

const { mouseX, mouseY } = useMousePosition()

onMounted(() => {
  const hoverItems = document.querySelectorAll(".cursor-hover-item")

  const title = document.querySelector(".title")
  const slices = document.querySelectorAll(".slice")
  // gsap.defaults({ ease: "none" })
  gsap.to({}, 0.016, {
    repeat: -1,
    onRepeat: () => {
      gsap.set(cursor.value, {
        css: {
          left: mouseX.value,
          top: mouseY.value,
        },
      })
    },
  })

  const { CircleType } = window
  let circleType = new CircleType(cursorTextEl.value)
  circleType.radius(50)

  setTimeout(() => {
    initialCursorHeight.value =
      circleType.container.style.getPropertyValue("height")
    // console.log(initialCursorHeight.value)
  }, 50)

  const updateCursor = () => {
    if (!isHovered) {
      gsap.to(cursorTextContainerEl.value, hoverEffectDuration.value * 0.5, {
        opacity: 0,
      })
      gsap.set(cursorTextContainerEl.value, {
        rotate: 0,
      })
    }
    requestAnimationFrame(updateCursor)
  }
  updateCursor()

  const handlePointerEnter = (e) => {
    isHovered.value = true
    const target = e.currentTarget

    gsap.set([cursorTextContainerEl.value, cursorTextEl.value], {
      height: initialCursorHeight.value,
      width: initialCursorHeight.value,
      mixBlendMode: "difference",
    })

    gsap.fromTo(
      cursorTextContainerEl.value,
      {
        rotate: 0,
      },
      {
        duration: cursorRotationDuration.value,
        rotate: 360,
        ease: "none",
        repeat: -1,
      }
    )

    gsap.to(cursorInner.value, hoverEffectDuration.value, {
      scale: 2,

      // backgroundColor: "red",
    })
    // gsap.fromTo(
    //   cursorInner.value,
    //   hoverEffectDuration.value,
    //   {
    //     backgroundColor: "#000",
    //   },
    //   { backgroundColor: "red" }
    // )

    gsap.fromTo(
      cursorTextContainerEl.value,
      hoverEffectDuration.value,
      {
        scale: 1.2,
        opacity: 0,
      },
      {
        delay: hoverEffectDuration.value * 0.75,
        scale: 1,
        opacity: 1,
      }
    )
    gsap.to(cursorOuter.value, hoverEffectDuration.value, {
      scale: 1.2,
      opacity: 0,
    })
  }

  const handlePointerLeave = () => {
    isHovered.value = false
    gsap.to([cursorInner.value, cursorOuter.value], hoverEffectDuration.value, {
      scale: 1,
      opacity: 1,
    })
    gsap.to(cursorTextContainerEl.value, hoverEffectDuration.value, {
      scale: 0,
      opacity: 0,
    })
    gsap.to(cursorInner.value, hoverEffectDuration.value, {
      // backgroundColor: "#000",
    })
  }

  title.addEventListener("pointerenter", () => {
    slices.forEach((slice) => {
      slice.style.transform = "translateY(0)"
      slice.style.opacity = 1
    })
  })

  title.addEventListener("pointerleave", () => {
    slices.forEach((slice) => {
      slice.style.transform = ""
      slice.style.opacity = 0
    })
  })

  hoverItems.forEach((item) => {
    item.addEventListener("pointerenter", handlePointerEnter)
    item.addEventListener("pointerleave", handlePointerLeave)

    item.addEventListener("mousemove", () => {
      // console.log(item.classList)
      cursor.value.classList.add("grow")
      if (item.classList.contains("big")) {
        cursor.value.classList.remove("grow")
        cursor.value.classList.add("grow-big")
      }
    })

    item.addEventListener("mouseleave", () => {
      cursor.value.classList.remove("grow")
      cursor.value.classList.remove("grow-big")
    })
  })
})
</script>

<template lang="pug">
.cursor(ref='cursor') 
  .cursor--small(ref='cursorInner') ♪
  .cursor--large(ref='cursorOuter') 
  .cursor--text(ref='cursorTextContainerEl')
    //- .text(ref='cursorTextEl') ➤➤➤➤➤➤➤➤➤➤➤➤➤➤➤➤➤➤➤
    .text(ref='cursorTextEl') Do Re Mi Fa Sol La Si Do Re Mi Fa Sol La Si
</template>

<style lang="stylus" scoped>

.cursor
  position fixed
  z-index 1000
  .cursor--small,.cursor--large,.cursor--text
    position absolute
    left 0
    top 0
    transform translate(-50%,-50%)
    border-radius 50%
    pointer-events none
    user-select none

  .cursor--text
    font-size 0.75rem
    opacity 0

    .text
      color color_blue
      font-family sans-serif
      font-weight bold
  .cursor--small
    color color_blue
    font-size 2rem
  .cursor--large
    size(60px)
    border 2px solid color_blue


.grow, .grow-big
  mix-blend-mode difference
.grow-big
  transform scale(1.5)
</style>
