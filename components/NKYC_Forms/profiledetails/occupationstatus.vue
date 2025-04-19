<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }"> 
            <logo style="width: 40px; height: 40px;"/>
            <profile/>
        </div>
        
        <div class="flex justify-between  p-2 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            
            <!-- Marital Status -->
            <div class="w-full mt-4 px-2 p-1" v-if="activebox === 'marriedbox'">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                    Your occupation 
                </p>
                <p class="text-sm mt-3 text-gray-500 font-normal leading-6">
                    These details are required by SEBI to open your Demat account.
                </p>
                
                <div class="grid grid-cols-2 gap-2 mt-3">
                    <button v-for="option in options" :key="option.value"
                        @click="selectMaritalStatus(option.value)"
                        :class="[
                            'px-6 py-2 rounded-lg border-2 text-lg font-normal w-full transition-all',
                            selected === option.value
                                ? 'bg-blue-600 border-blue-600 text-white'
                                : 'bg-gray-200 border-gray-300 text-black'
                        ]">
                        {{ option.label }}
                    </button>
                </div>
            </div>

            <div class="w-full flex gap-2">
                <Button @click="back()" class="primary_color cursor-pointer border-0 text-white w-1/6 dark:bg-slate-900">
                <i class="pi pi-angle-left text-3xl dark:text-white"></i>
            </Button>
                <Button type="button" @click="handleButtonClick" :disabled="!selected"
                    class="primary_color wave-btn text-white w-5/6 py-4 text-xl border-0">
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

const deviceHeight = ref(0);
const activebox = ref('marriedbox');
const emit=defineEmits(['updateDiv']);
const buttonText = ref("Next");
const isAnimating = ref(false);
// Marital Status
const selected = ref(""); 
const options = [
    { label: "Agriculturist ", value: "Agriculturist " },
    { label: "Business", value: "Business" },
    { label: "Govt.Service", value: "Govt.Service" },
    { label: "Housewife", value: "Housewife" },
    { label: "Private Sector", value: "Private Sector" },
    { label: "Public Sector", value: "Public Sector" },
    { label: "Professional", value: "Professional" },
    { label: "Retired", value: "Retired" },
    { label: "Student", value: "Student" },
    { label: "Others", value: "Others" },
];

const selectMaritalStatus = (value) => {
    selected.value = value;
    
   
};

const back = () => {
    emit('updateDiv', 'tradingexperience');
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
        emit('updateDiv', 'income');
    }, 800); 
};
</script>
