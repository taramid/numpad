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

    onType = (event: Event, digit: Arabic) => {
      if (Event.Digit === event) {
        digits.value.push(digit as Arabic)
        emit('update:modelValue', answer.value)
      }
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
        xs:w-full sm:w-3/4
        h-80
      "
  >
    <Pad :event="Event.Digit" :digit="Arabic.Zero" v-on:hit="onType"/>
    <Pad :event="Event.Backspace" v-on:hit="onBackspace" class="col-span-2 text-red-500">&#9003;</Pad>
    <Pad :event="Event.Digit" :digit="Arabic.One" v-on:hit="onType"/>
    <Pad :event="Event.Digit" :digit="Arabic.Two" v-on:hit="onType"/>
    <Pad :event="Event.Digit" :digit="Arabic.Three" v-on:hit="onType"/>
    <Pad :event="Event.Digit" :digit="Arabic.Four" v-on:hit="onType"/>
    <Pad :event="Event.Digit" :digit="Arabic.Five" v-on:hit="onType"/>
    <Pad :event="Event.Digit" :digit="Arabic.Six" v-on:hit="onType"/>
    <Pad :event="Event.Digit" :digit="Arabic.Seven" v-on:hit="onType"/>
    <Pad :event="Event.Digit" :digit="Arabic.Eight" v-on:hit="onType"/>
    <Pad :event="Event.Digit" :digit="Arabic.Nine" v-on:hit="onType"/>
    <Pad :event="Event.Enter" v-on:hit="onSubmit" class="col-span-3">enter</Pad>
  </div>

</template>
