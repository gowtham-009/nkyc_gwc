<template>
  <div class="primary_color overflow-hidden h-screen">
    <!-- Box 1 -->
    <div
      class="w-full p-2 primary_color transition-all duration-300"
      :style="{ height: box1Height + 'px' }"
    >
    <div class="w-full px-2 py-2 flex justify-end items-center">
        <ThemeSwitch />
      </div>

      <div class="w-full flex justify-center items-center">
        <logo/>
      </div>
    </div>

    <!-- Box 2 -->
    <div
      v-show="showBox2"
      class="w-full p-2 flex flex-col justify-between bg-white rounded-t-3xl dark:bg-black transition-all duration-300"
      :style="{ height: box2Height + 'px' }"
    >
    <div class="w-full mt-2 px-3 flex flex-col justify-between">
        <div class="w-full">
          <p class="text-2xl font-medium dark:text-gray-400">Ready to get started?</p>
          <p class="leading-6 text-sm font-normal text-gray-500">Enter your number to help us set up your investment account</p>
        </div>

        <div class="w-full mt-4">
          <MobileInput v-model="mobileNumber" />
          
        </div>

        <div class="w-full mt-4">
          <Checkbox v-model="checkboxValue" />
        </div>

       
      </div>
      <div class="w-full">
        <p class="text-sm text-center mb-2 font-normal text-gray-500">
            By processing, you accept "Name" <span class="font-medium">Terms of Use</span> and <span class="font-normal">Privacy Policy</span>
          </p>
        <Button   ref="rippleBtn"
        :disabled="!mobileNumber || mobileNumber.length !== 10"
         @click="handleButtonClick()" class="primary_color  w-full text-white  py-4 text-xl border-0">
        {{ buttonText }}
        
      </Button>

      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import ThemeSwitch from '~/components/darkmode/darkmodesign.vue';
import MobileInput from '~/components/forminputs/mobileinput.vue';
import Checkbox from '~/components/forminputs/remembercheckbox.vue';
const { ourl } = useUrl();



const box1Height = ref(0);
const box2Height = ref(0);
const showBox2 = ref(false);

const emit = defineEmits(['updateDiv']);
const mobileNumber = ref('');
const checkboxValue = ref('');
const rippleBtn = ref(null)
const buttonText = ref("Continue");

onMounted(() => {
  const fullHeight = window.innerHeight;

  // Initial state: full height to box 1, box 2 hidden
  box1Height.value = fullHeight;
  box2Height.value = 0;
  showBox2.value = false;

  // After 2 seconds: show box 2 and animate heights
  setTimeout(() => {
    showBox2.value = true;
    box1Height.value = fullHeight * 0.3;
    box2Height.value = fullHeight * 0.7;
  }, 500);

  // Optional: handle resize
  window.addEventListener('resize', () => {
    const updatedHeight = window.innerHeight;
    if (!showBox2.value) {
      box1Height.value = updatedHeight;
      box2Height.value = 0;
    } else {
      box1Height.value = updatedHeight * 0.3;
      box2Height.value = updatedHeight * 0.7;
    }
  });
});


const sendmobileotp=async()=>{
  const apiurl=ourl.value+'send-mobile-otp.php'
  localStorage.setItem('mobilenumber', mobileNumber.value)
  const formData=new FormData()

  formData.append('mobileNo',mobileNumber.value)
  formData.append('otpCode','789564')
  try {
    const response=await fetch(apiurl,{
      method:'POST',
      body:formData
      
    })
    if(!response.ok){
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    else{
      const data=await response.json()
      if(data){
        emit('updateDiv', 'div2', mobileNumber.value);
      }
    }
  } catch (error) {
    console.error(error.message)
  }
}

const handleButtonClick = () => {
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
    sendmobileotp()
  }, 600)
};
 
</script>

<style scoped>

</style>
