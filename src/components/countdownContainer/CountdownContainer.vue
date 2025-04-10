<template>
    <div class="container-fluid">
        <div class="row">
            <CountdownTimer v-if="countdownActive" :target-date="selectedDate" />
        </div>
        <div class="col d-flex flex-column flex-sm-row justify-content-center mt-3 mb-3 gap-3">
            <StartCountdown :selected-date="selectedDate" @start-countdown="startCountdown"/>
        </div>
        <div class="col d-flex justify-content-center">
            <SelectDate @date-selected="handleDateSelected" />
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import CountdownTimer from '../countdownTimer/CountdownTimer.vue';
import StartCountdown from '../startCountdown/StartCountdown.vue';
import SelectDate from '../selectDate/SelectDate.vue';

const selectedDate = ref(null);
const countdownActive = ref(false);

const handleDateSelected = (date) => {
    selectedDate.value = date;
    console.log('Selected date:', selectedDate.value);
    countdownActive.value = false;
};

const startCountdown = () => {
  if (selectedDate.value) {
    countdownActive.value = true;
  }
};

</script>

<style scoped></style>