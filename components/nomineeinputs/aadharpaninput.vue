<template>
  <div class="w-full">
    <label for="id_number" class="text-gray-500 text-lg font-normal">Nominee's ID proof no</label>
    <InputText
      id="id_number"
      class="w-full py-2"
      v-model="panaadhar"
      variant="filled"
      @input="formatInput"
      inputmode="numeric"
      maxlength="20"
   
    
      autocomplete="off"
      autocorrect="off"
    />
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);

// Internal model
const panaadhar = ref(props.modelValue || '');

// Clean input to allow only digits
const formatInput = (event) => {
  const raw = event.target.value;
  const cleaned = raw.replace(/[^0-9]/g, '').slice(0, 20);
  panaadhar.value = cleaned;
  event.target.value = cleaned; // force update on mobile
};

// Watch and sync with parent
watch(panaadhar, (newValue) => {
  emit('update:modelValue', newValue);
});
</script>
