<script setup lang="ts">

// order is after:
// https://github.com/vuejs/pinia/blob/v2/packages/pinia/src/storeToRefs.ts

import {ref} from 'vue'

import Pad from './Pad.vue'

import {Event, Arabic} from './types'


const typed = ref('')

// defineProps<{
//   classes?: string
// }>()

</script>

<template>

  <h2>{{ typed }}</h2>

  <div
      class="
        grid grid-cols-3 gap-px
        select-none
        text-5xl text-slate-600
        bg-gray-300
        [&>*]:bg-white
        xs:w-full sm:w-3/4
        h-80
      "
  >
    <Pad :event="Event.Digit" :digit="Arabic.Zero"/>
    <Pad :event="Event.Backspace" class="col-span-2 text-red-500">&#9003;</Pad>
    <Pad :event="Event.Digit" :digit="Arabic.One" />
    <Pad :event="Event.Digit" :digit="Arabic.Two"/>
    <Pad :event="Event.Digit" :digit="Arabic.Three"/>
    <Pad :event="Event.Enter" class="col-span-3">enter</Pad>
  </div>

</template>
