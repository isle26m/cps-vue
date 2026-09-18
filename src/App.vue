<script setup>
import { ref } from 'vue';

const started = ref(false);
const clicks = ref(0);
const cps = ref(0);
const done = ref(false);

function toggleStart() {
  started.value = !started.value;
  done.value = false;
  if(started.value) {
    setTimeout(() => {
      cps.value = (clicks.value/5).toFixed(2);
      started.value = false;
      done.value = true;
      clicks.value = 0;
    }, 5000);
  }
}

function add() {
  clicks.value = clicks.value+1;
}
</script>

<template>
  <div class="w-full h-dvh flex justify-center items-center">
    <div class="flex flex-col gap-8 items-center">
      <h1 class="text-7xl">{{ clicks }}</h1>
      <button @click="toggleStart" v-show="!started" class="text-xl px-4 py-2 cursor-pointer bg-[#8fbcbb]">Start</button>
      <button class="bg-[#2e3440] px-32 py-16 cursor-pointer text-white" @click="add" v-show="started">Click me !</button>
      <h1 v-show="done" class="text-xl">Cps: {{ cps }}</h1>
    </div>
  </div>
</template>
