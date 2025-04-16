<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3" :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span @click="back()" >
          <i class="pi pi-angle-left text-2xl text-white dark:text-gray-500"></i>
        </span>
            <ThemeSwitch />
        </div>
        <div class="flex justify-between  p-2 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-2 px-2 p-1">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                    Link your bank account
                </p>

                <p class="text-md mt-1 text-gray-500 font-normal leading-6">
                    Please provide your bank account details to link your bank account with your trading account.
                </p>

                <div class="w-full   p-1">
                    
                    <div class="mt-1">
                        <span class="text-gray-500 text-md">Account no</span>
                    <Accno v-model="accno"/>
                    </div>

                   <div class="mt-1">
                    <span class="text-gray-500 text-md">IFSC code</span>
                    <IFSC v-model="ifsc" />
                   </div>

                   
                   <div class="mt-1">
                    <span class="text-gray-500 text-md">MICR code</span>
                    <MICR  v-model="micr"/>
                   </div>

                   <div class="mt-1">
                        <span class="text-gray-500 text-md">Bank name</span>
                    <Bankname v-model="bankname"/>
                    </div>

                   <div class="mt-1">
                    <span class="text-gray-500 text-md">MICR code</span>
                    <MICR  v-model="micr"/>
                   </div>

                   <div class="mt-1">
                    <p  class="text-gray-500 text-md font-normal leading-4">Bank Address</p>
                    <Address v-model="address"/>
                   </div>
                </div>
            </div>

            <div class="w-full " >
                <Button @click="handleButtonClick"   :disabled="!bankname || !accno || !ifsc || !micr || !address"
                 class="primary_color wave-btn w-full text-white  py-4 text-xl border-0">
                    {{ buttonText }}
                    <span v-if="isAnimating" class="wave"></span>
                </Button>
            </div>


        </div>

    </div>






</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import { ref, onMounted } from 'vue';
import Bankname from '~/components/NKYC_Forms/bankdetails/bankinputs/bankname.vue'
import Accno from '~/components/NKYC_Forms/bankdetails/bankinputs/accno.vue'

import IFSC from '~/components/NKYC_Forms/bankdetails/bankinputs/ifsc.vue'
import MICR from '~/components/NKYC_Forms/bankdetails/bankinputs/micr.vue'
import Address from '~/components/NKYC_Forms/bankdetails/bankinputs/address.vue'
const emit = defineEmits(['updateDiv']);
const deviceHeight = ref(0);
const isAnimating = ref(false);
const buttonText = ref("Continue");


const bankname = ref('');
const accno = ref('');
const ifsc = ref('');
const micr = ref('');
const address = ref('');

onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});





const handleButtonClick = () => {

    const bankdetails=[
        {
            bankname: bankname.value,
            accno: accno.value,
            ifsc: ifsc.value,
            micr: micr.value,
            address: address.value
        }
    ]
 isAnimating.value = true;
    setTimeout(() => {
      isAnimating.value = false;
      emit('updateDiv', 'bank4', bankdetails);
    }, 800); 
};




function back(){
    emit('updateDiv', 'submission','2');
}


</script>
