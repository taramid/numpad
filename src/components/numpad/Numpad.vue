<script setup lang="ts">

// order is after:
// https://github.com/vuejs/pinia/blob/v2/packages/pinia/src/storeToRefs.ts

import {ref, computed} from 'vue'

import Pad from './Pad.vue'

import {Event, Arabic} from './types'


const props = defineProps<{
  modelValue: number | null,
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', value: number | null): void
  (e: 'submit', value: number): void
}>()


const digits = ref<Array<Arabic>>([])

const answer = computed<number | null>(() => parseInt(digits.value.join(''), 10) || null)

const

    onDigit = (digit: Arabic) => {
      digits.value.push(digit)
      emit('update:modelValue', answer.value)
    },

    onBackspace = () => {
      digits.value.pop()
      emit('update:modelValue', answer.value)
    },

    onSubmit = () => {
      if (answer.value) {
        emit('submit', answer.value as number)
        digits.value = []
      }
    },

    onTap = (event: Event, digit?: Arabic) => {
      if (Event.Digit === event) {
        onDigit(digit as Arabic)
      } else if (Event.Backspace === event) {
        onBackspace()
      } else if (Event.Enter === event) {
        onSubmit()
      }
    }
;

</script>

<template>

  <div
      class="
        grid grid-cols-3 gap-px
        select-none
        text-5xl text-slate-600
        bg-gray-300
        [&>*]:bg-white
        w-full sm:w-3/4 md:w-3/5 lg:w-1/2 xl:w-2/5
        h-80
      "
  >
    <Pad @tap="onTap" :event="Event.Digit" :digit="Arabic.Zero"/>
    <Pad @tap="onTap" :event="Event.Backspace" class="col-span-2 text-red-500">&#9003;</Pad>
    <Pad @tap="onTap" :event="Event.Digit" :digit="Arabic.One"/>
    <Pad @tap="onTap" :event="Event.Digit" :digit="Arabic.Two"/>
    <Pad @tap="onTap" :event="Event.Digit" :digit="Arabic.Three"/>
    <Pad @tap="onTap" :event="Event.Digit" :digit="Arabic.Four"/>
    <Pad @tap="onTap" :event="Event.Digit" :digit="Arabic.Five"/>
    <Pad @tap="onTap" :event="Event.Digit" :digit="Arabic.Six"/>
    <Pad @tap="onTap" :event="Event.Digit" :digit="Arabic.Seven"/>
    <Pad @tap="onTap" :event="Event.Digit" :digit="Arabic.Eight"/>
    <Pad @tap="onTap" :event="Event.Digit" :digit="Arabic.Nine"/>
    <Pad @tap="onTap" :event="Event.Enter" class="col-span-3">enter</Pad>
  </div>

<!--  https://vuejs.org/guide/typescript/composition-api.html#typing-component-props-->
<!--  https://vuejs.org/guide/extras/reactivity-transform.html#reactive-props-destructure-->
<!--  https://vuejs.org/api/sfc-script-setup.html#typescript-only-features-->

</template>
