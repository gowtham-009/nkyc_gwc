<template>
  <div class="w-full h-screen flex justify-center items-center">
    <Button
      label="Click"
      class="ripple-button w-full px-4 py-4 text-white primary_color"
      @click="createRipple"
      ref="rippleBtn"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'

const rippleBtn = ref(null)

function createRipple(event) {
  const button = rippleBtn.value
  const circle = document.createElement('span')
  circle.classList.add('ripple')

  const rect = button.$el.getBoundingClientRect()
  const x = event.clientX - rect.left
  const y = event.clientY - rect.top

  circle.style.left = `${x}px`
  circle.style.top = `${y}px`

  button.$el.appendChild(circle)

  setTimeout(() => {
    circle.remove()
    alert('hi')
  }, 600)
}
</script>

<style>
.ripple-button {
  position: relative;
  overflow: hidden;
}

.ripple {
  position: absolute;
  border-radius: 50%;
  transform: scale(0);
  animation: ripple-animation 0.6s linear;
  background-color: rgba(255, 255, 255, 0.5);
  pointer-events: none;
  width: 100px;
  height: 100px;
  opacity: 1;
  z-index: 10;
}

@keyframes ripple-animation {
  to {
    transform: scale(4);
    opacity: 0;
  }
}
</style>
