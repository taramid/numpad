<script setup lang="ts">

import Numpad from './components/numpad/Numpad.vue'

import {ref, watch} from 'vue'

const answer = ref(null)

const onAnswer = (value: number | null) => console.log('the answer is ' + value);

watch(answer, (n, o) => console.log('change detected', n, o))

</script>

<template>
  <div>

    <h2>{{ answer || '...' }}</h2>

    <Numpad v-model="answer" @submit="onAnswer"/>

  </div>

</template>
