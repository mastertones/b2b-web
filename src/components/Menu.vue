<script setup>
import { computed, defineComponent, h, onMounted, ref } from "vue"
import { NMenu, NIcon, NButton, NDrawer, NDrawerContent } from "naive-ui"
import Cursor from "../components/Cursor.vue"
const activeKey = ref(null)

const renderIcon = (icon) => {
  return () => h(NIcon, null, { default: () => h(icon) })
}

const menuOptionsUp = [
  {
    // label: () =>
    //   h(
    //     "a",
    //     {
    //       href: "https://www.master-tones.com/",
    //       target: "_blank",
    //       rel: "noopenner noreferrer",
    //     },
    //     "Analog Audio Effect Modeling"
    //   ),
    label: "Analog Audio Effect Modeling",
    key: "analog-audio-effect-modeling",
    children: [
      {
        label: "Guitar Gears",
        key: "guitar-gears",
      },
      {
        label: "Mixing/Mastering Gears",
        key: "mixing/mastering-gears",
      },
    ],
    // icon: renderIcon(BookIcon),
  },
  {
    label: "Emulation",
    key: "emulation",
    children: [
      {
        label: "Speaker Emulation",
        key: "speaker-emulation",
      },
      {
        label: "Microphone Emulation",
        key: "microphone-emulation",
      },
      {
        label: "Earphone Emulation",
        key: "earphone-emulation",
      },
    ],
  },
  {
    label: () =>
      h(
        "a",
        {
          href: "https://www.master-tones.com/",
          target: "_blank",
          rel: "noopenner noreferrer",
        },
        "Earphone Enhancement"
      ),
    // label: "Earphone Enhancement",
    key: "earphone-enhancement",
  },
  {
    label: "Tone Creation",
    key: "tone-creation",
    children: [
      {
        label: "Tone Conversion",
        key: "tone-conversion",
      },
      {
        label: "Tone Matching",
        key: "tone-matching",
      },
    ],
  },
  {
    label: () =>
      h(
        "a",
        {
          href: "https://www.master-tones.com/",
          target: "_blank",
          rel: "noopenner noreferrer",
        },
        "Source Separation"
      ),
    key: "source-separation",
  },
  {
    label: "Music Analysis",
    key: "music-analysis",
    children: [
      {
        label: "Music Transcription",
        key: "music-transcription",
      },
      {
        label: "Chord Recognition",
        key: "chord-recognition",
      },
      {
        label: "Pitch Detection",
        key: "pitch-detection",
      },
      {
        label: "BPM",
        key: "bpm",
      },
    ],
  },
  {
    label: "Human Voice Modeling",
    key: "human-voice-modeling",
    children: [
      {
        label: "Singing Voice Conversion",
        key: "singing-voice-conversion",
      },
      {
        label: "Singing Voice Synthesis",
        key: "singing-voice-synthesis",
      },
      {
        label: "Speech Synthesis",
        key: "speech-synthesis",
      },
      {
        label: "Speech Conversion",
        key: "speech-conversion",
      },
    ],
  },
]

const menuOptionsDown = [
  {
    label: "Spatial Audio",
    key: "spatial-audio",
    children: [
      {
        label: "Binaural",
        key: "binaural",
      },
      {
        label: "HRTF",
        key: "hrtf",
      },
    ],
  },
  {
    label: "Quality Enhancement",
    key: "quality-enhancement",
    children: [
      {
        label: "Noise Reduction",
        key: "noise-reduction",
      },
      {
        label: "Super Resolution",
        key: "super-resolution",
      },
    ],
  },
  {
    label: "AI Post Production",
    key: "ai-post-production",
    children: [
      {
        label: "AI Mastering",
        key: "ai-mastering",
      },
      {
        label: "AI Mixing",
        key: "ai-mixing",
      },
    ],
  },
  {
    label: "Audio Plugin Dev",
    key: "Audio Plugin Dev",
    children: [
      {
        label: "Audio Effect: VST/VST3/AU/AAX, Standalone",
        key: "audio-effect: VST/VST3/AU/AAX,standalone",
      },
      {
        label: "Virtual Instrument: VSTi, Standalone",
        key: "virtual-instrument: VSTi, standalone",
      },
    ],
  },
  {
    label: "Licensing Service",
    key: "Audio Plugin Dev",
    children: [
      {
        label: "Cloud Activation",
        key: "cloud-activation",
      },
      {
        label: "Local Activation",
        key: "local-activation",
      },
    ],
  },
  {
    label: "Web Audio Dev",
    key: "web-audio-dev",
    children: [
      {
        label: "Web Audio",
        key: "web-audio",
      },
      {
        label: "Deployment",
        key: "deployment",
      },
    ],
  },
  {
    label: () =>
      h(
        "a",
        {
          href: "https://www.master-tones.com/",
          target: "_blank",
          rel: "noopenner noreferrer",
        },
        "UI/UX Design"
      ),
    key: "ui/ux-design",
  },
]

const horizontalMode = ref(true)

const handleHorizontalMode = (innerWidth) => {
  console.log(innerWidth)
  if (innerWidth <= 1440) {
    horizontalMode.value = false
  } else {
    horizontalMode.value = true
  }
}

const active = ref(false)
const placement = ref("")
const activate = (place) => {
  active.value = true
  placement.value = place
}

onMounted(() => {
  console.log(window.innerWidth)
  handleHorizontalMode(window.innerWidth)
  //通過註冊resize監聽器，實現對視窗大小的監聽
  window.addEventListener(
    "resize",
    (e) => {
      handleHorizontalMode(e.target.innerWidth)
    },
    false
  )
  //溢位resize監聽器
  window.removeEventListener("resize", (e) => {
    handleHorizontalMode(e.target.innerWidth)
  })
})
</script>

<template lang="pug">
//- Cursor
.menu
  n-button.hamburger.cursor-hover-item(@click="activate('left')")
    n-icon.icon
      svg(xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' viewbox='0 0 32 32' )
        path(d='M4 6h24v2H4z' fill='currentColor')
        path(d='M4 24h24v2H4z' fill='currentColor')
        path(d='M4 12h24v2H4z' fill='currentColor')
        path(d='M4 18h24v2H4z' fill='currentColor')


  n-drawer(v-model:show="active" :width="400" :placement="placement")
    n-drawer-content.cursor-hover-item(closable)
      n-menu( v-model:value="activeKey" mode="vertical" :options="menuOptionsUp"  :collapsed="false" )
  //- n-menu.cursor-hover-item.left( v-model:value="activeKey" mode="vertical" :options="menuOptionsUp"  :collapsed="false" v-else)
  //- n-menu.cursor-hover-item.bottom( v-model:value="activeKey" mode="horizontal" :options="menuOptionsDown"  dropdown-placement='top-end' )
  //- n-menu.cursor-hover-item.right( v-model:value="activeKey" mode="vertical" :options="menuOptionsDown"  dropdown-placement='top-end' v-else)
  .slices
    - for(let i=1;i<=10;i++)
      div(class=`slice slice-${i} cursor-hover-item`)
</template>

<style lang="stylus" scoped>
.menu
  position fixed
  size(,100vh)
  flex(space-between,,column)
  background-color colorSecondary  //mix-blend-mode difference 失效是因為底層要設置顏色,預設白色被視為透明
  .cursor-hover-item
    color #fff
  .hamburger
    position fixed
    left 0
    font-size 3rem
    margin 1rem
    color color_blue
    size(48px)
    flex()
    .n-button__content
      border none
      background-color none
      flex()
      .icon
        svg
        // pos()
          flex()
          position absolute
          left 8px
          top 8px


.slices
  overflow hidden
  size(800px)
  flex()
  position absolute
  top 50%
  transform translateY(-50%)
  background url("https://picsum.photos/id/"+random(10,20)+"/800") center center no-repeat
  background-size contain
  opacity 0.2
  z-index -1
  // &:hover
  //   .slice
  //     transform translateY(0)
  //     opacity 1
  .slice
    z-index 2
    size()
    // border 1px solid #000
    background url("https://picsum.photos/id/"+random(10,20)+"/800") center center no-repeat
    background-size 800px
    transition all 1s ease-in-out

  for n in (1..10)
    nullBase = n - 1
    .slice-{n}
      background-position (nullBase * -80)px 0
      transform translateY(-10%)
      opacity 0
  for n in (1..5)
    .slice-{n*2}
      transform translateY(10%)


// @media screen and (max-width: 1440px)
</style>
