<script setup lang="ts">

import {ref, computed} from 'vue'

import type {Event, Arabic} from './types'

const props = defineProps<{
  event: Event,
  digit?: number,
}>()

const emit = defineEmits<{
  (e: 'hit', ev: Event, digit?: Arabic): void
}>()

const
    bPlayHitAnimation = ref(false),
    bAnotherOne = ref(false);

const startHitAnimation = () => {
  bAnotherOne.value = !bAnotherOne.value
  bPlayHitAnimation.value = true
}

const onHit = () => {
  startHitAnimation()
  emit('hit', props.event, props.digit)
}

const hitAnimation = computed(() => {
  if (bPlayHitAnimation.value) {
    return !bAnotherOne.value ? 'tap-0' : 'tap-1'
  }
  return ''
})

</script>

<template>
  <div
      :class="[
        'grid justify-center content-center',
        hitAnimation,
      ]"
      @click="onHit"
  >
    <slot>{{ props.digit ?? '_' }}</slot>
  </div>
</template>

<style scoped>

.tap-0 {
  animation: tap-frames-0 600ms;
}

@keyframes tap-frames-0 {
  0% {
    background-color: #ff8;
  }
  100% {
    background-color: white;
  }
}

.tap-1 {
  animation: tap-frames-1 600ms;
}

@keyframes tap-frames-1 {
  0% {
    background-color: #ff8;
  }
  100% {
    background-color: white;
  }
}

/* https://css-tricks.com/restart-css-animation/ */

</style>
