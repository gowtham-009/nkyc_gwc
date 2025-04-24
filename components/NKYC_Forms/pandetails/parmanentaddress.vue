<template>
    <div class="primary_color">
      <div
        class="flex justify-between primary_color items-center px-3"
        :style="{ height: deviceHeight * 0.08 + 'px' }"
      >
        <logo style="width: 40px; height: 40px;" />
        <profile />
      </div>
  
      <div
        class="flex justify-between p-2 flex-col bg-white rounded-t-3xl dark:bg-black"
        :style="{ height: deviceHeight * 0.92 + 'px' }"
      >
        <div class="w-full mt-2 p-1 px-2">
          <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
            Verify your Permanent address
          </p>
          <p class="text-sm mt-2 leading-6 text-gray-500 font-normal">
            Please confirm your address as per the documents you have uploaded.
          </p>
  
          <div class="w-full mt-1">
            <Address v-model="address" />
          </div>
          <div class="w-full mt-1">
            <State v-model="state" />
          </div>
          <div class="w-full mt-1">
            <City v-model="city" />
          </div>
          <div class="w-full mt-1">
            <Pincode v-model="pincode" />
          </div>
          <div class="w-full mt-1">
            <Addresscheck ref="commAddressRef" />
          </div>
        </div>
  
        <div class="w-full flex gap-2">
          <Button
            @click="back"
            ref="rippleBtnback"
            class="primary_color cursor-pointer border-0 text-white w-1/6 dark:bg-slate-900"
          >
            <i class="pi pi-angle-left text-3xl dark:text-white"></i>
          </Button>
  
          <Button
            type="button"
            @click="handleButtonClick"
            ref="rippleBtn"
            :disabled="!address || !state || !city || !pincode"
            class="primary_color wave-btn text-white w-5/6 py-4 text-xl border-0"
          >
            {{ buttonText }}
            <span v-if="isAnimating" class="wave"></span>
          </Button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import Address from '~/components/NKYC_Forms/pandetails/paninputs/address.vue';
  import State from '~/components/NKYC_Forms/pandetails/paninputs/state.vue';
  import City from '~/components/NKYC_Forms/pandetails/paninputs/city.vue';
  import Pincode from '~/components/NKYC_Forms/pandetails/paninputs/pincode.vue';
  import Addresscheck from '~/components/NKYC_Forms/pandetails/paninputs/confirmcheckbox.vue';
  
  const emit = defineEmits(['updateDiv']);
  const props = defineProps({
    data: {
      type: Object,
      required: true
    }
  });
  

  const address = ref(props.data.KYC_DATA.APP_COR_ADD1?props.data.KYC_DATA.APP_COR_ADD1 : '');
  const state = ref('');
  const city = ref(props.data.KYC_DATA.APP_COR_CITY?props.data.KYC_DATA.APP_COR_CITY : '');
  const pincode = ref(props.data.KYC_DATA.APP_COR_PINCD?props.data.KYC_DATA.APP_COR_PINCD :'');
  const deviceHeight = ref(window.innerHeight);
  const commAddressRef = ref(null);
  
  const buttonText = ref('Continue');
  const rippleBtn = ref(null);
  const rippleBtnback = ref(null);
  const isAnimating = ref(false);
  
  if (props.data && props.data.KYC_DATA?.APP_COR_STATE) {
    const stateCode = String(props.data.KYC_DATA.APP_COR_STATE);
    state.value = props.data.statelist[stateCode] || '';
  }
  
  onMounted(() => {
    const updateHeight = () => {
      deviceHeight.value = window.innerHeight;
    };
    window.addEventListener('resize', updateHeight);
  });
  
  const handleButtonClick = (event) => {
    animateRipple(rippleBtn.value, event);
    setTimeout(() => {
      if (!commAddressRef.value?.confirm) {
        emit('updateDiv', 'communicationaddress');
      } else {
        emit('updateDiv', 'submission', '1');
      }
    }, 600);
  };
  
  const back = (event) => {
    animateRipple(rippleBtnback.value, event);
    setTimeout(() => {
      emit('updateDiv', 'pandetails');
    }, 600);
  };
  
  function animateRipple(buttonRef, event) {
    const button = buttonRef?.$el || buttonRef;
    const circle = document.createElement('span');
    circle.classList.add('ripple');
  
    const rect = button.getBoundingClientRect();
    circle.style.left = `${event.clientX - rect.left}px`;
    circle.style.top = `${event.clientY - rect.top}px`;
  
    button.appendChild(circle);
    setTimeout(() => circle.remove(), 600);
  }
  </script>
  
  <style scoped>
  .ripple {
    position: absolute;
    background: rgba(255, 255, 255, 0.6);
    border-radius: 50%;
    transform: scale(0);
    animation: ripple-animation 0.6s linear;
    width: 100px;
    height: 100px;
    pointer-events: none;
  }
  
  @keyframes ripple-animation {
    to {
      transform: scale(2.5);
      opacity: 0;
    }
  }
  
  .p-checkbox-checked .p-checkbox-icon {
    color: white !important;
  }
  </style>
  