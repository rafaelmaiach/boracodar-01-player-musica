<template>
  <div class="container">
    <main class="player">
      <MusicInformation />
      <MusicTracking />
    </main>
  </div>

</template>

<script setup lang="ts">
  import MusicInformation from "./components/MusicInformation.vue";
  import MusicTracking from "./components/MusicTracking.vue";
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  width: 270px;
  padding: 38px;
  border-radius: 10px;
  background-color: var(--purple);
}

.player {
  padding: 12px 0;
}

@media (min-width: 48em) {
  .container {
    width: 400px;
    padding: 29px;
  }
}
</style>
