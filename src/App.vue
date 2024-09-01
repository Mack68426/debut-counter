<script setup>
import { ref, onMounted } from 'vue'

const targetDate = ref(new Date('2024-09-13T20:00:00+08:00'))
const timeLeft = ref({
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0
})

function updateCountdown() {
  const now = new Date()
  const difference = targetDate.value - now

  if (difference > 0) {
    timeLeft.value = {
      days: Math.floor(difference / (1000 * 60 * 60 * 24)),
      hours: Math.floor((difference / (1000 * 60 * 60)) % 24),
      minutes: Math.floor((difference / 1000 / 60) % 60),
      seconds: Math.floor((difference / 1000) % 60)
    }
  } else {
    timeLeft.value = { days: 0, hours: 0, minutes: 0, seconds: 0 }
  }
}

onMounted(() => {
  updateCountdown()
  setInterval(updateCountdown, 1000) // 每秒更新一次
})
</script>

<template>
  <div class="container">
    <h1>可可初配信倒數計時</h1>
    <p>距離 {{ targetDate.toLocaleString() }} 還有：</p>
    <div class="countdown">
      <div class="time-unit">
        <span class="number">{{ timeLeft.days }}</span>
        <span class="label">天</span>
      </div>
      <div class="time-unit">
        <span class="number">{{ timeLeft.hours.toString().padStart(2, "0") }}</span> 
        <span class="label">時</span>
      </div>
      <div class="time-unit">
        <span class="number">{{ timeLeft.minutes.toString().padStart(2, "0") }}</span>
        <span class="label">分</span>
      </div>
      <div class="time-unit">
        <span class="number">{{ timeLeft.seconds.toString().padStart(2, "0") }}</span>
        <span class="label">秒</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  text-align: center;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.countdown {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin-top: 20px;
}

.time-unit {
  display: flex;
  flex-direction: column;
}

.number {
  font-size: 48px;
  font-weight: bold;
}

.label {
  font-size: 16px;
  margin-top: 5px;
}
</style>