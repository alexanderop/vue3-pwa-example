<script setup lang="ts">
import { ref } from 'vue'

const time = ref(0)
const isRunning = ref(false)
let interval: number | null = null

function startTimer() {
  if (!isRunning.value) {
    isRunning.value = true
    interval = setInterval(() => {
      time.value++
    }, 1000)
  }
}

function stopTimer() {
  if (isRunning.value) {
    isRunning.value = false
    if (interval) {
      clearInterval(interval)
    }
  }
}

function resetTimer() {
  stopTimer()
  time.value = 0
}

function formatTime(seconds: number): string {
  const minutes = Math.floor(seconds / 60)
  const remainingSeconds = seconds % 60
  return `${minutes.toString().padStart(2, '0')}:${remainingSeconds.toString().padStart(2, '0')}`
}
</script>

<template>
  <div class="container">
    <h1>Vue 3 PWA Timer</h1>
    <div class="timer">{{ formatTime(time) }}</div>
    <div class="controls">
      <button @click="startTimer" :disabled="isRunning">Start</button>
      <button @click="stopTimer" :disabled="!isRunning">Stop</button>
      <button @click="resetTimer">Reset</button>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  font-family: Arial, sans-serif;
}

.timer {
  font-size: 4rem;
  margin: 2rem 0;
}

.controls {
  display: flex;
  gap: 1rem;
}

button {
  padding: 0.5rem 1rem;
  font-size: 1rem;
  cursor: pointer;
}
</style>