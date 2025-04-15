<template>
    <div class="w-full">
      <label for="pan_label" class="text-gray-500 text-lg font-normal">Address</label>
      <Textarea v-model="address" varient="filled" rows="3" class="w-full" cols="10"  />
    </div>
  </template>
  
  <script setup>
  import { ref, watch } from 'vue';
  
  const props = defineProps(['modelValue']);
  const emit = defineEmits(['update:modelValue']);
  
  const address = ref(props.modelValue || '');
  
 
  watch(address, (newValue) => {
    emit('update:modelValue', newValue);
  });
  </script>
  