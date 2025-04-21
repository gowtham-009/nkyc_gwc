<template>
  <div class="w-full h-screen flex justify-center items-center">
    <div class="input-wrapper">
    
    <InputText
      v-model="phone"
      placeholder="Your Mobile Number"
      class="prime-input py-5"
    />
    <span class="bottom-border"></span>
  </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import InputText from 'primevue/inputtext'

const phone = ref('')
</script>

<style scoped>
.input-wrapper {
  position: relative;
  display: flex;
  align-items: center;
  background-color: #f7f9fc;

  border-radius: 10px;
  overflow: hidden;
}



/* Style PrimeVue InputText */
.prime-input {
  border: none;
  background: transparent;
  outline: none;
  font-size: 16px;
  flex: 1;
  z-index: 1;
  box-shadow: none !important;
}

.prime-input::placeholder {
  color: #a0aec0;
}

/* Bottom border animation */
.bottom-border {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  height: 3px;
  width: 0;
  background-color: #007bff;
  border-radius: 10px;
  transition: 
    width 0.4s ease-out,
    height 0.3s ease-in;
  z-index: 0;
}

.input-wrapper:focus-within .bottom-border {
  width: 100%;
  height: 4px;
}
</style>
