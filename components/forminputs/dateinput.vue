<template>
  <div class="w-full">
    <label for="dob">DOB</label>
    <DatePicker v-model="date" showIcon dateFormat="dd/mm/yy" class="w-full" placeholder="As per PAN DOB - DD/MM/YYYY"/>
  </div>
</template>

<script setup>
 import { ref } from 'vue';
const props = defineProps(['modelValue']);
  const emit = defineEmits(['update:modelValue']);
  
  const date = ref(props.modelValue || '');
  watch(date, (newValue) => {
    emit('update:modelValue', newValue);
  });
</script>

<style >

</style>