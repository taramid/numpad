<script setup lang="ts">

import {Event, Arabic} from './types'

const props = defineProps<{
  event: Event,
  digit?: number,
}>()

const emit = defineEmits<{
  (e: 'hit', ev: Event, digit?: Arabic): void
}>()

</script>

<template>
  <div
      class="grid justify-center content-center"
      @click="emit('hit', props.event, props.digit)"
  >
    <slot>{{ props.digit ?? '_' }}</slot>
  </div>
</template>
