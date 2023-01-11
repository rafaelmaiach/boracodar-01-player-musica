<template>
  <button class="button" @click="handleAction">
    <component :is="icon"/>
  </button>
</template>

<script setup lang="ts">
import type { Component } from "vue";

interface Props {
  handleAction: VoidFunction
  icon: Component
}

defineProps<Props>()
</script>

<style scoped>
.button {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
  width: 25px;
  height: 25px;
}
</style>