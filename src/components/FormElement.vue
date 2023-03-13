<script setup>
import { ref, computed } from 'vue'

const $emit = defineEmits(['add:seconds'])

const seconds = ref(0)
const minutes = ref(0)

const isValidMinute = computed(() => minutes.value % 1 === 0 && minutes.value > 0)
const isValidSeconds = computed(() => seconds.value % 10 === 0 && seconds.value > 0)

const addSeconds = () => {
  if (!isValidMinute.value && !isValidSeconds.value) return
  $emit('add:seconds', seconds.value + minutes.value * 60)

  seconds.value = 0;
  minutes.value = 0;
}
</script>

<template>
  <div class="form">
    <label class="form__label">Укажите минуты с шагом 1</label>
    <input
      type="number"
      v-model="minutes"
      class="form__input"
      :class="{ 'form__input--error': !isValidMinute }"
    />
    <label class="form__label">Укажите секунды с шагом 10</label>
    <input
      type="number"
      v-model="seconds"
      class="form__input"
      :class="{ 'form__input--error': !isValidSeconds }"
    />
    <button class="form__btn" @click="addSeconds">Добавить таймер</button>
  </div>
</template>

<style lang="scss" scoped>
.form {
  display: flex;
  flex-direction: column;
  gap: rem(10px);

  &__input {
    border: 1px solid gray;
    padding: rem(5px 10px);
    line-height: rem(35px);
    outline: none;
    border-radius: rem(10px);

    &--error {
      border-color: red;
    }
  }

  &__btn {
    border: 1px solid gray;
    background: none;
    padding: rem(5px 10px);
    line-height: rem(35px);
    border-radius: rem(10px);
    cursor: pointer;
    transition: color 0.5s, background-color 0.5s;

    &:hover {
      background: gray;
      color: white;
    }
  }
}
</style>
