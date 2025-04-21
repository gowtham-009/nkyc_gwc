<template>
  <div class="input-wrapper">
    <InputText
      id="email"
      class="prime-input"
      v-model="email"
      variant="filled"
      placeholder="Your Email ID"
      size="large"
      @blur="validateEmail"
       autocomplete="off"
    />
    <span class="bottom-border"></span>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import InputText from 'primevue/inputtext';

const props = defineProps({
  modelValue: String
});
const emit = defineEmits(['update:modelValue']);

const email = ref(props.modelValue || '');

watch(email, (newVal) => {
  emit('update:modelValue', newVal);
});

const validateEmail = () => {
  const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailPattern.test(email.value)) {
    console.log('Please enter a valid email address');
    // You can add error handling logic here if needed.
  }
};
</script>

<style scoped>
.input-wrapper {
  position: relative;
  display: flex;
  align-items: center;
  background-color: #e0e0e0;
  border-radius: 10px;
  padding: 0 0.75rem;
  overflow: hidden;
}

.prime-input {
  border: none;
  background: transparent;
  outline: none;
  font-size: 16px;
  flex: 1;
  padding: 1rem 0;
  z-index: 1;
  box-shadow: none !important;
}

.prime-input::placeholder {
  color: #87909b;
}

.bottom-border {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  height: 3px;
  width: 0;
  background-color: #007bff;
  border-radius: 10px;
  transition: width 0.4s ease-out, height 0.3s ease-in;
  z-index: 0;
}

.input-wrapper:focus-within .bottom-border {
  width: 100%;
  height: 4px;
}
</style>
