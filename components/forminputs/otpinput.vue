<template>
  <div class="card flex justify-center">
    <div class="flex flex-col items-center py-2">
      <div class="flex w-full" style="gap: 0">
        <input
          v-for="(digit, index) in otp"
          :key="index"
          ref="otpInputs"
          type="tel"
          inputmode="numeric"
          maxlength="1"
          class="custom-otp-input w-full dark:text-slate-100"
          v-model="otp[index]"
          @input="onInput(index, $event)"
          @keydown.backspace="onBackspace(index)"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, nextTick } from 'vue';

const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);

const length = 6;
const otp = ref(Array(length).fill(''));
const otpInputs = ref([]);

// Sync with prop
watch(() => props.modelValue, (val) => {
  if (val && val.length === length) {
    otp.value = val.split('');
  }
});

// Emit when OTP changes
watch(otp, (val) => {
  emit('update:modelValue', val.join(''));
}, { deep: true });

function onInput(index, event) {
  const value = event.target.value.replace(/\D/g, '');
  otp.value[index] = value;

  if (value && index < length - 1) {
    nextTick(() => otpInputs.value[index + 1]?.focus());
  }
}

function onBackspace(index) {
  if (otp.value[index] === '' && index > 0) {
    nextTick(() => otpInputs.value[index - 1]?.focus());
  }
}
</script>

<style scoped>
.custom-otp-input {
  height: 48px;
  font-size: 24px;
  appearance: none;
  text-align: center;
  transition: all 0.2s;
  border-radius: 0;
  border: 1px solid rgb(184, 183, 183);
  background: transparent;
  outline-offset: -2px;
  outline-color: transparent;
  transition: outline-color 0.3s;
}

.custom-otp-input:focus {
  outline: none;
}

.custom-otp-input:first-child {
  border-top-left-radius: 12px;
  border-bottom-left-radius: 12px;
}

.custom-otp-input:last-child {
  border-top-right-radius: 12px;
  border-bottom-right-radius: 12px;
}
</style>
