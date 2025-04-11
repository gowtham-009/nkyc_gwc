<template>
    <div class="primary_color" >
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span @click="back()" class="text-white cursor-pointer"><i class="pi pi-angle-left text-3xl"></i></span>
            <ThemeSwitch />
        </div>
        <div class="flex justify-between flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-4 px-5 p-1">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                   Personal details
                </p>

               <div class="w-full mt-2 p-1" >
                     <Name v-model="name" />
               </div>
               <div class="w-full mt-2 p-1" >
                        <Fathername v-model="fathername" />
               </div>
               <div class="w-full mt-2 p-1" >
                        <Dob v-model="dob" />
               </div>
               <div class="w-full mt-2 p-1" >
                <Gender v-model:selected="gender" />
               </div>
               <div class="w-full mt-2 p-1" >
                    <Address v-model="address" />
               </div>

               

               

              
            </div>

            <div class="w-full p-1 bg-gray-100 rounded-t-3xl dark:bg-gray-900">
              
                <Button type="button"  @click="handleButtonClick" :disabled="!name || !fathername || !dob || !gender || !address " 
                    class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  ">
                    {{ buttonText }}
                    <span v-if="isAnimating" class="wave"></span>
                </Button>
            </div>


        </div>

    </div>

   



   
</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import Name from '~/components/NKYC_Forms/pandetails/paninputs/name.vue'
import Fathername from '~/components/NKYC_Forms/pandetails/paninputs/fathername.vue'
import Dob from '~/components/NKYC_Forms/pandetails/paninputs/dateinput.vue'
import Gender from '~/components/NKYC_Forms/pandetails/paninputs/gender.vue'
import Address from '~/components/NKYC_Forms/pandetails/paninputs/address.vue'

import { ref, onMounted } from 'vue';

const emit = defineEmits(['updateDiv']);
const deviceHeight = ref(0);
const buttonText = ref("Continue");
const isAnimating = ref(false);

const name = ref('');
const fathername = ref('');
const dob=ref('');
const gender=ref('');
const address = ref('');    


onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});


const handleButtonClick = () => {
  
 isAnimating.value = true;
    setTimeout(() => {
      isAnimating.value = false;
     console.log( name.value, fathername.value, dob.value, gender.value, address.value);
      emit('updateDiv', 'digilockerconfirmation'); 
    }, 800); 
};





const back = () => {
    emit('updateDiv', 'digilockersubmission'); 
};






</script>
