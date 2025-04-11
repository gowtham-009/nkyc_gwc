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
                   Cofirm your address
                </p>

                <p class="text-md mt-2 leading-6 text-gray-500 font-normal">
                   Please confirm your address as per the documents you have uploaded.
                </p>
               

                <div class="w-full mt-2">
                    <Address v-model="address"/>
                </div>
                <div class="w-full mt-2">
                    <State v-model="state"/>
                </div>
                <div class="w-full mt-2">
                    <City v-model="city"/>
                </div>
                <div class="w-full mt-2">
                    <Pincode v-model="pincode"/>
                </div>

              
            </div>

            <div class="w-full p-1 bg-gray-100 rounded-t-3xl dark:bg-gray-900">
              
                <Button type="button"  @click="handleButtonClick" :disabled="!address || !state || !city || !pincode" 
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
import Address from '~/components/NKYC_Forms/pandetails/paninputs/address.vue'
import State from '~/components/NKYC_Forms/pandetails/paninputs/state.vue'
import City from '~/components/NKYC_Forms/pandetails/paninputs/city.vue'
import Pincode from '~/components/NKYC_Forms/pandetails/paninputs/pincode.vue'
import { ref, onMounted } from 'vue';

const emit = defineEmits(['updateDiv']);
const deviceHeight = ref(0);
const buttonText = ref("Continue");
const isAnimating = ref(false);

const address = ref('');
const state = ref('');
const city = ref('');
const pincode = ref('');

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
     
      emit('updateDiv', 'pandetails'); 
    }, 800); 
};





const back = () => {
    emit('updateDiv', 'digilockerconfirmation'); 
};






</script>
