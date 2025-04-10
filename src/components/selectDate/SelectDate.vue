<template>
    <DatePicker 
        class="w-25 rounded p-2" 
        variant="filled"
        placeholder="Select date"
        v-model="selectedDate" 
        showIcon
        fluid
        :showOnFocus="false"
        dateFormat="dd/mm/yy"
        @update:model-value="emitSelectedDate" />
</template>

<script setup>
import DatePicker from 'primevue/datepicker'
import { ref } from 'vue'

const selectedDate = ref(null);
const emit = defineEmits(['date-selected']);

const emitSelectedDate = () => {
    emit('date-selected', selectedDate.value);
}

</script>