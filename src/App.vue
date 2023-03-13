<script setup>
import { ref } from "vue";
import FormElement from './components/FormElement.vue'
import TimerItem from './components/TimerItem.vue'

const seconds = ref([]);

const addSeconds = (item) => {
  seconds.value.push(item);
}
</script>

<template>
  <main class="main">
    <FormElement @add:seconds="addSeconds"/>

    <ul class="main__timers">
      <li v-for="(item, index) in seconds" :key="index">
        #{{ index + 1 }}: <TimerItem :seconds="item" />
      </li>
    </ul>
  </main>
</template>

<style lang="scss" scoped>
.main {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: rem(20px);
  max-width: rem(1200px);
  margin: 0 auto;

  @include mobile {
    grid-template-columns: 1fr;
  }

  &__timers {
    padding: 0;
    li {
      display: flex;
      gap: rem(10px);
    }
  }
}
</style>
