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

                <div class="w-full mt-1 flex justify-between items-center">
                    <h2 class="font-medium text-md dark:text-gray-500">00:{{ timeLeft.toString().padStart(2, '0') }}s</h2>

                    <Button type="button" label="Resend"  @click="visible = true"  badgeSeverity="contrast" outlined />
                </div>
            </div>
          </div>
          <div class="w-full flex gap-2" >
            <Button @click="back()" class="primary_color cursor-pointer border-0 text-white w-1/6 dark:bg-slate-900">
                <i class="pi pi-angle-left text-3xl dark:text-white"></i>
            </Button>
            <Button
             type="button"
              label="Verify OTP"
               class="primary_color wave-btn text-white w-5/6 py-4 text-xl border-0"
                @click="mobile_signup()"  :disabled="!isOtpValid" >
                {{ buttonText }}
                <span v-if="isAnimating" class="wave"></span>
        </Button>
          </div>
        </div>


    </div>


    <Dialog v-model:visible="visible" modal header="Resend OTP" :style="{ width: '25rem' }">
   
        <div class="w-full flex items-center justify-center p-2" >
            <img src="https://cdn-icons-png.flaticon.com/128/5290/5290058.png" class="w-20 h-20" alt="">
            <p class="text-2xl font-medium">You OTP Sent</p>
        </div>
   
</Dialog>
</template>

<script setup>
import ThemeSwitch from '~/components/darkmode/darkmodesign.vue';
import phoneOTP from '~/components/forminputs/otpinput.vue'
import { ref, onMounted, watch, watchEffect, onUnmounted } from 'vue';
const deviceHeight = ref(0);
const emit = defineEmits(['updateDiv']);
const timeLeft = ref(60); // Start from 60 seconds
const phoneNumber = ref('')
const isAnimating = ref(false);
const buttonText = ref("Verify OTP");
let timer = null;
const visible = ref(false);
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
    isAnimating.value = true;
    setTimeout(() => {
      isAnimating.value = false;
      emit('updateDiv', 'div3');
    }, 800); 
}
const back=()=>{
    emit('updateDiv', 'div1');
}
</script>

<style>

</style>