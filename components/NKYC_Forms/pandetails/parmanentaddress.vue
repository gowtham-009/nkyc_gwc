<template>
    <div class="primary_color" >
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <ThemeSwitch />
        </div>
        <div class="flex justify-between p-2 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-2 p-1 px-2 ">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                   {{status}} your Permanent address
                </p>

                <p class="text-md mt-2 leading-6 text-gray-500 font-normal">
                   Please confirm your address as per the documents you have uploaded.
                </p>
               

                <div class="w-full mt-1">
                    <Address v-model="address"/>
                </div>
                <div class="w-full mt-1">
                    <State v-model="state"/>
                </div>
                <div class="w-full mt-1">
                    <City v-model="city"/>
                </div>
                <div class="w-full mt-1">
                    <Pincode v-model="pincode"/>
                </div>

                <div class="w-full mt-1">
                    <Addresscheck  ref="commAddressRef"/>
                </div>

            </div>

            <div class="w-full flex gap-2">
                <Button @click="back()" class="primary_color cursor-pointer text-white w-1/6 ">
                <i class="pi pi-angle-left text-3xl"></i>
            </Button>
                <Button type="button"  @click="handleButtonClick" :disabled="!address || !state || !city || !pincode" 
                    class=" primary_color wave-btn text-white w-5/6 py-4 text-xl border-0  ">
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
import Addresscheck from '~/components/NKYC_Forms/pandetails/paninputs/confirmcheckbox.vue'
import { ref, onMounted } from 'vue';
const status = ref('')
const emit = defineEmits(['updateDiv']);
const deviceHeight = ref(0);
const buttonText = ref("Continue");
const isAnimating = ref(false);
const props = defineProps({
    data: {
        type:String,
       
    },
});

if(props.data=='failed'){
  status.value='Fill'
}
else{
    status.value='Verify'
}

const address = ref('');
const state = ref('');
const city = ref('');
const pincode = ref('');

const commAddressRef = ref(null)
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
      if(!commAddressRef.value?.confirm){
        emit('updateDiv', 'communicationaddress'); 
      }
     else{
        emit('updateDiv', 'submission','1');
     }
    
    }, 800); 
};





const back = () => {
    emit('updateDiv', 'pandetails'); 
};






</script>
<style >
.p-checkbox-checked .p-checkbox-icon{
    color: white !important;
}
</style>