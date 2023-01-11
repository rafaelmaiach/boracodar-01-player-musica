<template>
  <div class="track-container">
    <div class="buttons-container">
      <MusicTrackingButton :handle-action="playBack" :icon="IconPlayBack" icon-alt="Play previous track"/>
      <MusicTrackingButton :handle-action="isPlayingTrack ? pause : play" :icon="isPlayingTrack ? IconPause : IconPlay"/>
      <MusicTrackingButton :handle-action="playForward" :icon="IconPlayForward" icon-alt="Play next track"/>
    </div>
    <div class="track-progress">
      <div class="track-progress-bar" :style="{ width: `${progress}%` }"></div>
    </div>
    <div class="track-time">
      <span class="track-time-current">{{ currentTimeLabel }}</span>
      <span class="track-time-total">{{ remainingTimeLabel }}</span>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from "vue";
import MusicTrackingButton from "./MusicTrackingButton.vue";
import {
  IconPause,
  IconPlay,
  IconPlayBack,
  IconPlayForward,
} from "../assets/icons";

const isPlayingTrack = ref(false)
const intervalRef = ref()

const randomizeTrack = () => Math.floor(Math.random() * 120) + 120

const progress = ref(0) // 0 to 100%
const totalTime = ref(randomizeTrack()) // seconds
const currentTime = ref(0) // seconds
const remainingTime = ref(totalTime.value) // seconds

const play = () => {
  isPlayingTrack.value = true

  if (remainingTime.value === 0) {
    currentTime.value = 0
    remainingTime.value = totalTime.value
    progress.value = 0
  }

  intervalRef.value = setInterval(() => {
    currentTime.value++
    remainingTime.value--
    progress.value = (currentTime.value / totalTime.value) * 100

    if (remainingTime.value === 0) {
      clearInterval(intervalRef.value)
      isPlayingTrack.value = false
    }
  }, 1000)
}

const pause = () => {
  isPlayingTrack.value = false

  if (intervalRef.value) {
    clearInterval(intervalRef.value)
  }
}

const playBack = () => {
  currentTime.value = 0
  remainingTime.value = totalTime.value
  progress.value = 0
}

const playForward = () => {
  pause()
  totalTime.value = randomizeTrack()
  currentTime.value = 0
  remainingTime.value = totalTime.value
}

const convertTimeToText = (time) => {
  const minutes = Math.floor(time / 60)
  const seconds = time % 60

  return `${ minutes.toString().padStart(2, "0") }:${seconds.toString().padStart(2, "0")}`
}

const currentTimeLabel = computed(() => {
  return convertTimeToText(currentTime.value)
})

const remainingTimeLabel = computed(() => {
  return convertTimeToText(remainingTime.value)
})
</script>

<style scoped>
.track-container {
  margin-top: 29px;
}

.buttons-container {
  display: flex;
  justify-content: space-between;
  margin-top: 29px;
}

.track-progress {
  width: 100%;
  height: 6px;
  background-color: var(--white-30);
  border-radius: 10px;
  margin-top: 29px;
}

.track-progress-bar {
  height: 100%;
  background-color: var(--white-80);
  border-radius: 10px;
}

.track-time {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
  color: var(--white-darker);
  font-size: 0.875rem;
  line-height: 160%;
  opacity: 0.7;
}
</style>
