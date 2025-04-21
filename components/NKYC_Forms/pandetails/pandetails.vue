<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <logo style="width: 40px; height: 40px;"/>
            <profile/>
        </div>
        <div class="flex justify-between  p-2 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-2 p-1 px-2">
                <p class="text-2xl  text-blue-950 font-medium dark:text-gray-400">
                    Enter your PAN detail
                </p>
                <p class="text-gray-500 leading-5 font-normal text-sm mt-2">These details are required by SEBI to open
                    your Demat account.</p>

                <div class="w-full mt-2">
                    <Paninput v-model="panno" />
                </div>

                <div class="w-full mt-2 flex gap-3">
                    <div class="w-full"><Aadhar v-model="aadhar" /></div>
                    <div class="w-full"><DOB v-model="dateval"/></div>
                    
                </div>


              

             

             

                <div class="w-full mt-2">
                    <Pancheck v-model="checkboxval" />
                </div>
              
                <div class="w-full flex gap-3 px-2 py-2 mt-2 bg-gray-100 rounded-lg dark:bg-gray-900">
                    <p><i class="pi pi-star-fill text-xl text-yellow-400"></i></p>
                    <p class=" text-gray-500 text-sm leading-5">Your account would be opened as per your PAN card
                        details. Plese use the <span class="font-normal">Offline Account Opening Form</span> if you are
                        looking to open an HUF, Corporate, Partnership, Joint or NRI account.</p>
                </div>
            </div>

            <div class="w-full flex gap-2" >
                <Button @click="back()" class="primary_color cursor-pointer border-0 text-white w-1/6 dark:bg-slate-900">
                <i class="pi pi-angle-left text-3xl dark:text-white"></i>
            </Button>
                <Button type="button" ref="rippleBtn" :disabled="!panno || !aadhar || !dateval" @click="handleButtonClick"
                    class=" primary_color wave-btn text-white w-5/6 py-4 text-xl border-0  ">
                    {{ buttonText }}
                </Button>
            </div>

        </div>
    </div>




</template>
<script setup>

import { ref, onMounted } from 'vue';
import Paninput from '~/components/NKYC_Forms/pandetails/paninputs/paninput.vue';
import Aadhar from '~/components/NKYC_Forms/pandetails/paninputs/aadhar.vue';

import DOB from '~/components/NKYC_Forms/pandetails/paninputs/dateinput.vue'
import Pancheck from '~/components/NKYC_Forms/pandetails/paninputs/pancheck.vue'


const props = defineProps({
    data: {
        type: Object,
        default: () => ({}),
    },
});


const deviceHeight = ref(0);
const rippleBtn = ref(null);
const buttonText = ref("Continue");
const panno = ref('')
const aadhar = ref('')
const dateval = ref('')
const checkboxval = ref('')


onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});
const emit = defineEmits(['updateDiv']);
const back = () => {

    emit('updateDiv', 'ekyc');
}



const handleButtonClick = () => {
  let statusvalue
   if(props.data=='failed'){
        statusvalue=props.data
   }
   else{
    statusvalue=''
   }
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
    emit('updateDiv', 'parmanentaddress', statusvalue);
  }, 600)
};
</script> 
