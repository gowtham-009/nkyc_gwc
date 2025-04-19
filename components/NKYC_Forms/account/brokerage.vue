<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }"> 
           
            <ThemeSwitch />
        </div>
        
        <div class="flex justify-between  p-2 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            
            <!-- Income Selection -->
            <div class="w-full mt-4 px-2 p-1">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                   Brokerage details
                </p>
                <p class="text-md mt-3 text-gray-500 font-normal leading-6">
                    These details are required by SEBI to open your Demat account.
                </p>


                <div class="w-full mt-2 px-4 py-2 rounded-lg bg-gray-200">
                    <p class="flex gap-2 items-center"><i class="pi pi-check text-xl text-green-500 font-semibold"></i> <span class="font-semibold text-lg text-gray-800">EQUITY DELIVERY</span><span class="text-md font-normal text-gray-500">:0.5%</span></p>
                    <p class="flex gap-2 items-center"><i class="pi pi-check text-xl text-green-500 font-semibold"></i> <span class="font-semibold text-lg text-gray-800">EQUITY INTRADAY</span><span class="text-md font-normal text-gray-500">:0.1%</span></p>
                    <p class="flex gap-2 items-center"><i class="pi pi-check text-xl text-green-500 font-semibold"></i> <span class="font-semibold text-lg text-gray-800">EQUITY FUTURES</span><span class="text-md font-normal text-gray-500">:0.05%</span></p>
                    <p class="flex gap-2 items-center"><i class="pi pi-check text-xl text-green-500 font-semibold"></i> <span class="font-semibold text-lg text-gray-800">EQUITY OPTIONS</span><span class="text-md font-normal text-gray-500">:RS.100 PER LOT OR ORDER</span></p>
                    <p class="flex gap-2 items-center"><i class="pi pi-check text-xl text-green-500 font-semibold"></i> <span class="font-semibold text-lg text-gray-800">MCX FUTURES</span><span class="text-md font-normal text-gray-500">:0.06%</span></p>
                    <p class="flex gap-2 items-center"><i class="pi pi-check text-xl text-green-500 font-semibold"></i> <span class="font-semibold text-lg text-gray-800">MCX OPTIONS</span><span class="text-md font-normal text-gray-500">:RS.100 PER LOT</span></p>

                </div>
                
              
            </div>

            <!-- Submit Button -->
            <div class="w-full flex gap-2">
                <Button @click="back()" class="primary_color cursor-pointer text-white w-1/6 ">
                <i class="pi pi-angle-left text-3xl"></i>
            </Button>
                <Button 
                    type="button"  
                    @click="handleButtonClick" 
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
import ThemeSwitch from '~/components/darkmode/darkmode.vue';

const emit = defineEmits(['updateDiv']);

const deviceHeight = ref(0);

const buttonText = ref("Next");
const isAnimating = ref(false);




const back = () => {
    emit('updateDiv', 'tradingsegment');
};

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
       
        emit('updateDiv', 'uploadproof'); 
    }, 800);
};
</script>
