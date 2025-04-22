<template>
  <div class="primary_color">
    <div class="w-full px-3 primary_color flex justify-between items-center" :style="{ height: deviceHeight * 0.08 + 'px' }">
   
        <logo style="width: 40px; height: 40px;"/>
        <ThemeSwitch />
     
     
    </div>

    <div class="w-full flex flex-col justify-between p-2 bg-white rounded-t-3xl dark:bg-black" :style="{ height: deviceHeight * 0.92 + 'px' }">
      <div class="w-full mt-2 px-3">
        <div class="w-full">
          <p class="text-2xl font-medium dark:text-gray-400">Add your email</p>
          <p class=" leading-6 text-sm font-normal text-gray-500">
            This is where we'll send you important updates and insights on the market.
          </p>
        </div>

        <div class="w-full mt-4">
          <EmailInput v-model="emailid" />

        </div>
      </div>

      <div class="w-full flex gap-2">
        <Button @click="back()" ref="rippleBtnback" class="primary_color cursor-pointer border-0 text-white w-1/6 dark:bg-slate-900">
                <i class="pi pi-angle-left text-3xl dark:text-white"></i>
            </Button>
          <Button type="button"  ref="rippleBtn"
           label="Continue" :disabled="!isValidEmail"
            class="  primary_color text-white w-5/6 py-4 text-xl border-0 "
            @click="handleButtonClick">
            {{ buttonText }}
          
          </Button>

        
        </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import ThemeSwitch from '~/components/darkmode/darkmodesign.vue';
import EmailInput from '~/components/forminputs/emailinput.vue';
import Button from 'primevue/button';

const { url } = useUrl();

const rippleBtn = ref(null)
const emailid = ref('');
const emit = defineEmits(['updateDiv']);
const deviceHeight = ref(0);
const rippleBtnback = ref(null)
const buttonText = ref("Continue");
onMounted(() => {
  deviceHeight.value = window.innerHeight;
  window.addEventListener('resize', () => {
    deviceHeight.value = window.innerHeight;
  });

  
});

// Function to validate email format
const isValidEmail = computed(() => {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(emailid.value);
});

const sendemailotp=async()=>{
  const apiurl=url.value+'send-email-otp.php'
 
  const formData=new FormData()

  formData.append('emailId',emailid.value)
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
      if(data.Message=='OK'){
        emit('updateDiv', 'div4', emailid.value)
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
    sendemailotp()
  }, 600)
};

const back = () => {

  const button = rippleBtnback.value
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
    emit('updateDiv', 'div2');
  }, 600)
 
};
</script>
