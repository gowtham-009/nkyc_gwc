<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }"> 
            <span @click="back()" class="text-white cursor-pointer">
                <i class="pi pi-angle-left text-3xl"></i>
            </span>
            <ThemeSwitch />
        </div>
        
        <div class="flex justify-between  p-2 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            
            <!-- Income Selection -->
            <div class="w-full mt-4 px-2 p-1" >
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                    Upload proofs
                </p>
                <p class="text-md mt-3 text-gray-500 font-normal leading-6">
                    These details are required by SEBI to open your Demat account.
                </p>
                
              

               
                    <div class="w-full mt-2">
                        <span class="text-gray-500 text-xl font-medium mb-2">Upload Documents</span>
                        <div class="grid grid-cols-2 gap-5 ">
                        <div >
                            <PAN v-model:src="imageSrcpan"/>
                        </div>
                        <div >
                            <SIGNATURE v-model:src="imageSrcsign"/>
                        </div>
                        <div >
                            <BANK v-model:src="imageSrcbank"/>
                        </div>
                        <div >
                            <INCOME   v-model:src="fileSrc"
    v-model:isImage="isImage"
    v-model:isPdf="isPdf"/>

  
                        </div>
                    </div>
                    </div>

                    <div class="w-full mt-3">
                    <Select v-model="selectedstatement" :options="statement" optionLabel="name" placeholder="Choose Income Proof" class="w-full md:w-56" />
                </div>
                
             
            </div>

            <!-- Submit Button -->
            <div class="w-full mt-6">
                <Button 
  type="button"  
  @click="handleButtonClick" 
  :disabled="!selectedstatement || !imageSrcpan || !imageSrcsign || !imageSrcbank || !fileSrc || (!isImage && !isPdf)"
  class="primary_color wave-btn text-white w-full py-4 text-xl border-0"
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
import PAN from '~/components/NKYC_Forms/account/fileuploads/pancard.vue';
import SIGNATURE from '~/components/NKYC_Forms/account/fileuploads/signature.vue';
import BANK from '~/components/NKYC_Forms/account/fileuploads/bankproof.vue';
import INCOME from '~/components/NKYC_Forms/account/fileuploads/incomeproof.vue';
const emit = defineEmits(['updateDiv']);

const deviceHeight = ref(0);

const buttonText = ref("Next");
const isAnimating = ref(false);

const fileSrc = ref(null)
const isImage = ref(false)
const isPdf = ref(false)

const imageSrcpan = ref(null)
const imageSrcsign=ref(null)
const imageSrcbank=ref(null)

const selectedstatement = ref();
const statement = ref([
    { name: 'BANK STATEMENTS' },
    { name: 'NETWORTH CERTIFICATE' },
    { name: 'FORM 16' },
    { name: 'ITR COPY' },
    { name: 'PAYSLIP' },
    { name: 'DP HOLDING STATEMENTS' }
]);

const back = () => {
    emit('updateDiv', 'brokerage');
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
        
       emit('updateDiv', 'submission', '4'); 
    }, 800);
};
</script>
