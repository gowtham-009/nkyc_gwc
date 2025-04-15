<template>
    <div class="primary_color" >
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span @click="back()" class="text-white cursor-pointer"><i class="pi pi-angle-left text-3xl"></i></span>
            <ThemeSwitch />
        </div>
        <div class="flex justify-between p-2 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-4 px-2 p-1">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                   Client information
                </p>

               <div class="w-full mt-2 p-1" >
                     <Father v-model="father" />
               </div>
               <div class="w-full mt-2 p-1" >
                        <Mother v-model="mother" />
               </div>
         

             
               

               

              
            </div>

            <div class="w-full bg-gray-100 rounded-t-3xl dark:bg-gray-900">
              
                <Button type="button"  @click="handleButtonClick" :disabled="!father || !mother  "  
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
import Father from '~/components/NKYC_Forms/profiledetails/profileinputs/father.vue'
import Mother from '~/components/NKYC_Forms/profiledetails/profileinputs/mother.vue'
import { ref, onMounted } from 'vue';

const emit = defineEmits(['updateDiv']);
const deviceHeight = ref(0);
const buttonText = ref("Next");
const isAnimating = ref(false);


const father = ref('');
const mother = ref('');



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
      emit('updateDiv', 'qualification'); 
    }, 800); 
};





const back = () => {
    emit('updateDiv', 'info'); 
};






</script>
