<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3" 
            :style="{ height: deviceHeight * 0.08 + 'px' }">
          <logo style="width: 40px; height: 40px;"/>
            <ThemeSwitch/>
        </div>
        <div class="flex justify-between  p-2 flex-col bg-white rounded-t-3xl dark:bg-black" 
            :style="{ height: deviceHeight * 0.92 + 'px' }">
          <div class="w-full p-1 mt-2" >
            <p class="font-medium text-slate-800 text-2xl dark:text-gray-400">
                OTP sent
            </p>
            <p class="text-sm leading-6  font-normal text-gray-500">
                We have sent an OTP to your mobile number +91 {{ phoneNumber }}
            </p>
            <div class="w-full mt-3">
                <phoneOTP v-model="p_otp"/>
                <div class="w-full h-8">
                    <p class="text-lg font-medium text-center text-gray-500" v-if="resend_sh">OTP Resend Successfully +91 {{ phoneNumber }}</p>
                </div>
                <div class="w-full flex justify-between items-center">
                    <h2 class="font-medium text-md dark:text-gray-500">00:{{ timeLeft.toString().padStart(2, '0') }}s</h2>
                   <span @click="resendotp" class="text-xl font-medium text-blue-500 ">Resend</span>
                </div>
            </div>
          </div>
          <div class="w-full flex gap-2" >
            <Button @click="back()" class="primary_color cursor-pointer border-0 text-white w-1/6 dark:bg-slate-900">
                <i class="pi pi-angle-left text-3xl dark:text-white"></i>
            </Button>
            <Button  ref="rippleBtn"
             type="button"
              label="Verify OTP"
               class="primary_color  text-white w-5/6 py-4 text-xl border-0"
                @click="mobile_signup()"  :disabled="!isOtpValid" >
                {{ buttonText }}
        </Button>
          </div>
        </div>


    </div>


   
</template>

<script setup>
import ThemeSwitch from '~/components/darkmode/darkmodesign.vue';
import phoneOTP from '~/components/forminputs/otpinput.vue'
import { ref, onMounted, watch, watchEffect, onUnmounted } from 'vue';
const deviceHeight = ref(0);
const emit = defineEmits(['updateDiv']);
const timeLeft = ref(60); // Start from 60 seconds
const phoneNumber = ref('')
const rippleBtn = ref(null)
const buttonText = ref("Verify OTP");
let timer = null;

const p_otp=ref('')
const props = defineProps({
    data: {
        type: Object,
        default: () => ({}),
    },
});

onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });

  
 timer = setInterval(() => {
        if (timeLeft.value > 0) {
            timeLeft.value -= 1;
        } else {
            clearInterval(timer);
        }
    }, 1000);



});

onUnmounted(() => {
    clearInterval(timer);
});

watchEffect(() => {
    const mobileNo = props.data || '';
 
    phoneNumber.value = mobileNo.length >= 10
        ? `${mobileNo.slice(0, 2)}******${mobileNo.slice(-3)}`
        : mobileNo;

   
});

const isOtpValid = computed(() => 
p_otp.value.length === 6
);

const mobile_signup=()=>{
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
    emit('updateDiv', 'div3');
  }, 600)
} 
const back=()=>{
    emit('updateDiv', 'div1');
}

const resend_sh=ref(false)
const resendotp=()=>{
  resend_sh.value=true
}
</script>

<style>

</style>