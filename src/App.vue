<script setup>
import { ref, reactive, computed } from 'vue'
const John = {
  height: 170,
  weight: 60
}

const vueJohn = reactive(John)
 
vueJohn.BMI = computed(() => vueJohn.weight / (vueJohn.height / 100) / (vueJohn.height / 100))

const eat = () => {
  vueJohn.weight += 5
}
</script>

<template>
  <button @click="eat">eat</button>
  <p>height: {{ vueJohn.height }}</p>
  <p>weight: {{ vueJohn.weight }}</p>
  <p>BMI: {{ vueJohn.BMI }}</p>
</template>
