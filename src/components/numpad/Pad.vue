<script setup lang="ts">

import {Event} from './types'

const props = defineProps<{
  event: Event,
  digit?: number,
}>()

const onHit = () => console.log(props.event, props.digit);

</script>

<template>
  <div
      class="grid justify-center content-center"
      @click="onHit"
  >
    <slot>{{ props.digit ?? '_' }}</slot>
  </div>
</template>
