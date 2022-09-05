<script setup lang="ts">

import {ref} from 'vue'

import type {Event, Arabic} from './types'

const props = defineProps<{
  event: Event,
  digit?: number,
}>()

const emit = defineEmits<{
  (e: 'hit', ev: Event, digit?: Arabic): void
}>()

const bPlayHitAnimation = ref(false)

const startHitAnimation = () => {
  bPlayHitAnimation.value = false
  setTimeout(
      () => bPlayHitAnimation.value = true,
      0
  )
}

const onHit = () => {
  startHitAnimation()
  emit('hit', props.event, props.digit)
}

</script>

<template>
  <div
      :class="{
        'grid justify-center content-center' : true,
        'tap': bPlayHitAnimation
      }"
      @click="onHit"
  >
    <slot>{{ props.digit ?? '_' }}</slot>
  </div>
</template>

<style scoped>

.tap {
  animation: tap-frames 1200ms;
}

@keyframes tap-frames {
  0% {
    /* background-image: radial-gradient(#ffa, #ff8); gradient is not animatable */
    background-color: #ff8;
  }
  100% {
    background-color: white;
  }
}

</style>
