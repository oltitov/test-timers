<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  seconds: {
    type: Number,
    required: true,
    validator(value) {
      return value >= 10
    }
  }
})

const responseTime = new Date(Date.now() + 1000 * props.seconds)
const currentTimer = ref('')
let requestAnimationFrameId = false

const startTimer = () => {
  const t = responseTime - Date.now()
  const miliSeconds = `000${Math.floor(t % 1000)}`.slice(-3)
  const seconds = `00${Math.floor((t / 1000) % 60)}`.slice(-2)
  const minutes = `00${Math.floor((t / 1000 / 60) % 60)}`.slice(-2)

  currentTimer.value = `${minutes}:${seconds}:${miliSeconds}`

  if (t <= 0) {
    const finishHours = `00${responseTime.getHours()}`.slice(-2)
    const finishMinutes = `00${responseTime.getMinutes()}`.slice(-2)
    const finishSeconds = `00${responseTime.getSeconds()}`.slice(-2)
    currentTimer.value = `00:00:000 - ${finishHours}:${finishMinutes}:${finishSeconds}`

    return cancelAnimationFrame(requestAnimationFrameId)
  }

  requestAnimationFrame(startTimer)
}

onMounted(() => {
  requestAnimationFrameId = requestAnimationFrame(startTimer)
})

onUnmounted(() => {
  cancelAnimationFrame(requestAnimationFrameId)
})
</script>

<template>
  <div class="timer">
    {{ currentTimer }}
  </div>
</template>
