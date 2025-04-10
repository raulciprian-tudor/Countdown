<template>
    <button class="btn btn-success" 
        :disabled="!selectedDate" 
        @click="onStartCountdown">Start Countdown</button>
</template>

<script setup>
    import { defineProps, defineEmits } from 'vue';

    const props = defineProps({
       selectedDate: Date
    });

    const emit = defineEmits();

    const onStartCountdown = () => {
        if (props.selectedDate) {
            emit('start-countdown');
        }
    };
</script>