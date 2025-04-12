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
            <div class="w-full mt-4 px-2 p-1">

                <div class="w-full flex justify-center">
                    <img src="https://cdn-icons-png.flaticon.com/128/2830/2830289.png" alt="">
                </div>

                <h1 class="text-center mt-3 text-2xl font-medium text-blue-950 dark:text-gray-400">
                    Bank account added
                </h1>
                <p class="text-md text-center mt-1 font-normal text-gray-500">
                    Your bank details have been verified.
                </p>

                <div class="mt-3 w-full px-2 py-3 bg-gray-100 rounded-lg dark:bg-gray-900">
                    <div class="w-full flex items-center gap-2">
                        <div
                            class="p-2 px-2 flex justify-center items-center static w-14 h-14 bg-blue-200 dark:bg-slate-900  rounded-full  flex-shrink-0">
                            <span><i class="pi pi-building-columns text-blue-900 text-3xl md:text-4xl"></i></span>
                        </div>

                        <div>
                            <p class="text-medium text-lg text-gray-500">{{ bankname }}</p>
                        </div>

                    </div>

                    <div class="w-full flex mt-2 p-1" >
                        <div class="w-full p-1" >
                            <p class="text-md text-left text-gray-500 font-normal">Acc.No.</p>
                        </div>
                        <div class="w-full p-1" >
                            <p class="text-lg text-right text-blue-900 font-medium dark:text-gray-400">{{accno}}</p>
                        </div>
                    </div>
                    <div class="w-full flex p-1" >
                        <div class="w-full p-1" >
                            <p class="text-md text-left text-gray-500 font-normal">IFSC Code</p>
                        </div>
                        <div class="w-full p-1" >
                            <p class="text-lg text-right text-blue-900 font-medium dark:text-gray-400">{{ifsccode}}</p>
                        </div>
                    </div>
                    <div class="w-full flex p-1" >
                        <div class="w-full p-1" >
                            <p class="text-md text-left text-gray-500 font-normal">MICR CODE</p>
                        </div>
                        <div class="w-full p-1" >
                            <p class="text-lg text-right text-blue-900 font-medium dark:text-gray-400">{{ MICR }}</p>
                        </div>
                    </div>

                    <div class="w-full flex p-1" >
                        <div class="w-full p-1" >
                            <p class="text-md text-left text-gray-500 font-normal">Address</p>
                        </div>
                        <div class="w-full p-1" >
                            <p class="text-lg text-right text-blue-900 font-medium dark:text-gray-400">{{ address }}</p>
                        </div>
                    </div>
                </div>
            </div>

            <div class="w-full" >
                <Button type="button"  @click="handleButtonClick" 
                    class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  ">
                    {{ buttontext }}
                    <span v-if="isAnimating" class="wave"></span>
                </Button>
            </div>


        </div>

    </div>






</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import { ref, onMounted, defineProps } from 'vue';

const emit = defineEmits(['updateDiv']);

const props = defineProps({
  data: {
    type: Array,
    required: true
  }
})


const bankname = ref(props.data[0].bankname || '');
const accno = ref(props.data[0].accno || '');
const ifsccode = ref(props.data[0].ifsc || '');
const MICR = ref(props.data[0].micr || '');
const address = ref(props.data[0].address || '');



const deviceHeight = ref(0);
const buttontext =ref('Continue')
const isAnimating = ref(false);
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
      emit('updateDiv', 'submission', '3');
    }, 800); 
};


function back(){
    emit('updateDiv', 'bank1');
}







</script>
