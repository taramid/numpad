<script setup lang="ts">

import {reactive, computed} from 'vue'

import type {Event, Arabic} from './types'

const props = defineProps<{
  event: Event,
  digit?: number,
}>()

const emit = defineEmits<{
  (e: 'tap', ev: Event, digit?: Arabic): void
}>()

const animation = reactive({
  bPlay: false,
  n: 0,
  swap() {
    this.n = 1 - this.n
    this.bPlay = true
  },
  name() {
    if (this.bPlay) {
      return 'tap-animation-' + this.n
    }
  }
})

const onTap = () => {
  animation.swap();
  emit('tap', props.event, props.digit)
}

const tapAnimation = computed(() => animation.name())

</script>

<template>
  <div
      :class="[
        'grid justify-center content-center',
        tapAnimation,
      ]"
      @click="onTap"
  >
    <slot>{{ props.digit ?? '_' }}</slot>
  </div>
</template>

<style scoped>

.tap-animation-0 {
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

.tap-animation-1 {
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
