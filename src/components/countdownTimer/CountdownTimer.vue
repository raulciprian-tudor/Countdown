<template>
    <div v-if="timeRemaining > 0" class="text-center col d-flex justify-content-center align-items-center">
        <div>
            <p class="text-center m-0 text-uppercase fw-bold">Days</p>
            <span class="countdown-timer">{{ formattedDays }}</span>
        </div>
        <div class="divider"></div>
        <div>
            <p class="text-center m-0 text-uppercase fw-bold">Time remaining</p>
            <span class="countdown-timer">{{ formattedTime }}</span>
        </div>
    </div>
    <div v-else class="text-center">
        <p class="text-center">Countdown complete!</p>
    </div>
</template>

<script setup>
import './CountdownTimer.scss'
import { ref, watchEffect } from 'vue'

const props = defineProps({
    targetDate: Date
})

const timeRemaining = ref(0)
const formattedTime = ref('')
const formattedDays = ref('')

const calculateTimeRemaining = () => {
    if (!props.targetDate) return;

    const now = new Date();
    const target = new Date(props.targetDate);
    const diff = target - now;
    timeRemaining.value = Math.max(Math.floor(diff / 1000), 0);

    const days = Math.floor(timeRemaining.value / (3600 * 24));
    const hours = Math.floor((timeRemaining.value % (3600 * 24)) / 3600);
    const minutes = Math.floor((timeRemaining.value % (3600)) / 60);
    const seconds = Math.floor(timeRemaining.value % 60);

    formattedDays.value = `${String(days).padStart(2, '0')}`;
    formattedTime.value = `${String(hours).padStart(2, '0')}:${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
}

watchEffect(() => {
    if (!props.targetDate) return;

    calculateTimeRemaining();
    const interval = setInterval(() => {
        calculateTimeRemaining();
        if (timeRemaining.value <= 0) {
            clearInterval(interval);
        }
    }, 1000);
})
</script>