<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <logo style="width: 40px; height: 40px;"/>
            <profile/>
        </div>
        <div class="flex justify-between  p-2 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-2 px-2">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                    Complete your e-KYC
                </p>
                <p class="text-gray-500 leading-5 mt-3 font-normal text-sm">
                    Make sure your mobile number is linked to your Aadhaar card.
                </p>

                <li class="list-none mt-2"><a href="" class="text-blue-900 font-normal text-sm underline">How to link
                        Aadhaar with mobile?</a></li>


                <div class="w-full mt-3 px-2 py-2 rounded-lg bg-gray-100 dark:bg-gray-900">


                    <div class="w-full flex items-center gap-3 p-1 mt-2">
                        <div  class="p-2 px-2 flex justify-center items-center static w-10 h-10 bg-gray-200 rounded-md flex-shrink-0 dark:bg-gray-800">
                            <span><i class="pi pi-file-arrow-up text-xl text-blue-600"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="font-normal leading-5 text-sm text-gray-500">
                                You will be redirected to Digilocker for e-KYC.
                            </p>
                        </div>
                    </div>

                    <div class="w-full flex items-center gap-3 p-1 mt-2">
                        <div  class="p-2 px-2 flex justify-center items-center static w-10 h-10 bg-gray-200 rounded-md flex-shrink-0 dark:bg-gray-800">
                            <span><i class="pi pi-users text-xl text-blue-600"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="font-normal leading-5 text-sm text-gray-500">
                                It is a Govt of India initiative with more than 176.75 million trusted users.
                            </p>
                        </div>
                    </div>

                    <div class="w-full flex items-center gap-3 p-1 mt-2">
                        <div
                            class="p-2 px-2 flex justify-center items-center static w-10 h-10 bg-gray-200 rounded-md flex-shrink-0 dark:bg-gray-800">
                            <span><i class="pi pi-id-card text-xl text-blue-600"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="font-normal leading-5 text-sm text-gray-500">
                                You won't need to enter your details manually as the required documents will be fetched
                                from Digilocker.
                            </p>
                        </div>
                    </div>
                </div>


            </div>

            <div class="w-full flex gap-2" >
                <Button @click="back()" class="primary_color cursor-pointer border-0 text-white w-1/6 dark:bg-slate-900">
                <i class="pi pi-angle-left text-3xl dark:text-white"></i>
            </Button>
                <Button type="button"  @click="handleButtonClick"
                    class=" primary_color wave-btn text-white w-5/6 py-4 text-xl border-0  ">
                    {{ buttonText }}
                    <span v-if="isAnimating" class="wave"></span>
                </Button>
            </div>


        </div>

    </div>
</template>
<script setup>

import { ref, onMounted } from 'vue';

const deviceHeight = ref(0);
const isAnimating = ref(false);
const buttonText = ref("Start e-KYC");
onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});




const emit = defineEmits(['updateDiv']);
const back = () => {

    emit('updateDiv', 'nkyclist');
}


const handleButtonClick = () => {
 isAnimating.value = true;
    setTimeout(() => {
      isAnimating.value = false;
      emit('updateDiv', 'digilockersubmission');
    }, 800); 
};







</script>
