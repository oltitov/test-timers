<script setup>
import { ref, computed } from 'vue'

const $emit = defineEmits(['add:seconds'])

const seconds = ref(0)
const minutes = ref(0)

const isValidMinute = computed(() => minutes.value % 1 > 0)
const isValidSeconds = computed(() => seconds.value % 10 > 0)

const addSeconds = () => {
  if (!isValidMinute.value || !isValidSeconds.value) return
  return $emit('add:seconds', seconds.value)
}
</script>

<template>
  <div class="form">
    <label>Укажите минуты с шагом 1</label>
    <input type="integer" v-model="minutes" :class="{ 'form__input--error': isValidMinute }" />
    <label>Укажите секунды с шагом 10</label>
    <input type="integer" v-model="seconds" :class="{ 'form__input--error': isValidSeconds }" />
    <button @click="addSeconds">Добавить таймер</button>
  </div>
</template>
