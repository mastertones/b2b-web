<script setup>
import { defineComponent, h, ref } from "vue"
import { NMenu, NIcon } from "naive-ui"
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
    //       href: "https://en.wikipedia.org/wiki/Hear_the_Wind_Sing",
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
          href: "https://en.wikipedia.org/wiki/Hear_the_Wind_Sing",
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
          href: "https://en.wikipedia.org/wiki/Hear_the_Wind_Sing",
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
          href: "https://en.wikipedia.org/wiki/Hear_the_Wind_Sing",
          target: "_blank",
          rel: "noopenner noreferrer",
        },
        "UI/UX Design"
      ),
    key: "ui/ux-design",
  },
]
</script>

<template lang="pug">
//- Cursor
.menu
  n-menu.cursor-hover-item( v-model:value="activeKey" mode="horizontal" :options="menuOptionsUp"  )
  n-menu.cursor-hover-item( v-model:value="activeKey" mode="horizontal" :options="menuOptionsDown"  dropdown-placement='top-end')

  .slices
    - for(let i=1;i<=10;i++)
      div(class=`slice slice-${i} cursor-hover-item`)
</template>

<style lang="stylus" scoped>
.menu
  position fixed
  size(,100vh)
  flex(space-between,,column)
  // background-color colorSecondary  //mix-blend-mode difference 失效是因為底層要設置顏色,預設白色被視為透明
  .cursor-hover-item
    color #fff
.slices
  overflow hidden
  size(800px)
  flex()
  position absolute
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
</style>
