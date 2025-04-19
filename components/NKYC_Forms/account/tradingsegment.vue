<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }"> 
            <logo style="width: 40px; height: 40px;"/>
            <profile/>
        </div>
        
        <div class="flex justify-between  p-2 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            
            <!-- Income Selection -->
            <div class="w-full mt-4 px-2 p-1" >
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                    Trading Segment
                </p>
                <p class="text-md mt-3 text-gray-500 font-normal leading-6">
                    These details are required by SEBI to open your Demat account.
                </p>
                
                <div class="grid grid-cols-2 gap-2 mt-3">
                    <button 
                        v-for="option in options" 
                        :key="option.value"
                        @click="toggleSelection(option.value)"
                        :class="[
                            'px-6 py-2 rounded-lg border-2 text-lg font-normal w-full transition-all',
                            selected.includes(option.value)
                                ? 'bg-blue-600 border-blue-600 text-white'
                                : 'bg-gray-200 border-gray-300 text-black'
                        ]"
                    >
                        {{ option.label }}
                    </button>
                </div>
            </div>

            <!-- Submit Button -->
            <div class="w-full flex gap-2">
                <Button @click="back()" class="primary_color cursor-pointer border-0 text-white w-1/6 dark:bg-slate-900">
                <i class="pi pi-angle-left text-3xl dark:text-white"></i>
            </Button>
                <Button 
                    type="button"  
                    @click="handleButtonClick" 
                    :disabled="selected.length === 0"
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

const selected = ref([]); // Allow multiple selections

const options = [
    { label: "NSE CASH", value: "NSE CASH" },
    { label: "BSE CASH", value: "BSE CASH" },
    { label: "NSE F & O", value: "NSE F & O" },
    { label: "BSE F & O", value: "BSE F & O" },
    { label: "NSE CD", value: "NSE CD" },
    { label: "BSE CD", value: "BSE CD" },
    { label: "MCX", value: "MCX" },
    { label: "MCX CD", value: "MCX CD" },
    { label: "NSE COMMODITIES", value: "NSE COMMODITIES" },
    { label: "BSE COMMODITIES", value: "BSE COMMODITIES" },
];

const toggleSelection = (value) => {
    const index = selected.value.indexOf(value);
    if (index === -1) {
        selected.value.push(value); // Add to selection
    } else {
        selected.value.splice(index, 1); // Remove from selection
    }
};

const back = () => {
    emit('updateDiv', 'submission', '3');
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
        console.log(selected.value)
       emit('updateDiv', 'brokerage'); 
    }, 800);
};
</script>
