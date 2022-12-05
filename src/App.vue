<script setup>
import CountdownHeader from '@/components/CountdownHeader.vue'
import CountdownSegment from './components/CountdownSegment.vue'
import { useNow } from '@vueuse/core'
import { reactive, computed } from 'vue'

const now = useNow()
const christmas = new Date('12/25/2022 00:00:00')

const countdown = computed(() => {
  // get total seconds between the times
  var delta = Math.abs(christmas - now.value) / 1000

  // calculate (and subtract) whole days
  var days = Math.floor(delta / 86400)
  delta -= days * 86400

  // calculate (and subtract) whole hours
  var hours = Math.floor(delta / 3600) % 24
  delta -= hours * 3600

  // calculate (and subtract) whole minutes
  var minutes = Math.floor(delta / 60) % 60
  delta -= minutes * 60

  // what's left is seconds
  var seconds = Math.floor(delta % 60)

  return {
    days,
    hours,
    minutes,
    seconds,
  }
})
</script>
<template>
  <div class="w-full h-full flex justify-center items-center p-10">
    <div>
      <div class="shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px]">
        countdown: {{ countdown }}
        <CountdownHeader />
        <main class="flex justify-center">
          <CountdownSegment label="days" :number="countdown.days" />
          <CountdownSegment label="hours" :number="countdown.hours" />
          <CountdownSegment label="minutes" :number="countdown.minutes" />
          <CountdownSegment label="seconds" :number="countdown.seconds" />
        </main>
      </div>
      <h4 class="mt-10 text-gray-400 text-center text-sm">
        This challenge brought to you by <a href="https://vueschool.io/" class="underline">Vue School</a>
      </h4>
    </div>
  </div>
</template>

<style>
div {
  display: block;
}

body {
  @apply bg-gray-100;
}
</style>
