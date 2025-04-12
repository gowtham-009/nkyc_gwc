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

            <!-- Marital Status -->
            <div class="w-full mt-4 px-2 p-1">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                    Add nominee
                </p>
                <p class="text-md mt-1 text-gray-500 font-normal leading-6">
                    Relationship with nominee
                </p>
                <div class="w-full flex flex-col gap-2 mt-3">

                    <div v-if="nomineescard"  class="w-full p-2 bg-gray-200 rounded-lg">
                        <span class="text-gray-500">Nominee's relationship:{{ relationship_c }}</span> <br>
                        <span class="text-gray-500">Nominee's name: {{ name_c }}</span><br>
                        <span class="text-gray-500">Nominee's Date of birth: {{ dob_c }}</span><br>
                        <span class="text-gray-500">Nominee's Address:{{ address_c }}</span>
                    </div>
                    <Button @click="visible = true"
                        class="w-full py-3 primary_color text-white">
                    {{ nomineetext }}
                    </Button>

                    <p v-if="skip" class="text-center text-md text-blue-600 mt-2">Skip now</p>
                </div>
            </div>
            <Dialog class="p-0" v-model:visible="visible" modal  header="Add Nominee" :style="{ width: '25rem' }">

             <div class="w-full">
                <Name v-model="name"  />
             </div>
               <div class="w-full mt-2">
                <Namemode  v-model:relationship="selectedRelationship"  />
               </div>
               <div class="w-full mt-2">
                <DOB v-model="dob"  />
               </div>
               <div class="w-full mt-2">
                <span class="text-lg text-gray-500">Select Id proof</span>
                <Proof v-model:selected="idProof" />
               </div>
                <div class="w-full mt-2">
                    <Aadharpan v-model="aadharpan"  />
                </div>
               
               <div class="w-full mt-2">
                <Address v-model="address"  />
               </div>
              
               <div class="w-full mt-2">
                <span class="text-lg text-gray-500">Available shares {{ sharevalue }}</span>
                <Sharevalue v-model="shareval"/>
               </div>

               <!-- <div class="w-full mt-2">
                <span class="text-gray-500 text-lg">
                    Upload a file (optional)
                </span>
                <FileUpload ref="fileupload" class="text-white" mode="basic" name="demo[]" url="/api/upload" accept="image/*" :maxFileSize="1000000" @upload="onUpload" />
               </div>
              -->

                <div class="w-full mt-3">
                    <Button :disabled="!selectedRelationship || !name || !dob || !aadharpan || !address || !idProof || !shareval " label="Save" @click="nomineesave()" class="primary_color w-full text-white py-2"></Button>
                </div>
            </Dialog>


            <div class="w-full">
                <Button @click="handleButtonClick"
                    class="primary_color wave-btn w-full text-white  py-4 text-xl border-0">
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
import Namemode from '~/components/nomineeinputs/dropdown.vue';
import Name from '~/components/nomineeinputs/nameinput.vue';
import DOB from '~/components/nomineeinputs/dateinput.vue'
import Aadharpan from '~/components/nomineeinputs/aadharpaninput.vue';
import Address from '~/components/nomineeinputs/address.vue';
import Proof from '~/components/nomineeinputs/proofcheckbox.vue';
import Sharevalue from '~/components/nomineeinputs/sharevalue.vue';
const sharevalue=ref(100)
const shareval=ref('')
const skip=ref(true);
const visible = ref(false);
const emit=defineEmits(['updateDiv']);
const deviceHeight = ref(0);
const isAnimating = ref(false);
const buttonText = ref("Continue");
const nomineetext = ref("Add Nominee");
const idProof = ref('')
const selectedRelationship = ref(null);
const name = ref('');
const dob = ref('');
const aadharpan = ref('');
const address = ref('');

const nomineescard=ref(false)

const relationship_c=ref('')
const name_c=ref('')
const dob_c=ref('')
const address_c=ref('')

const fileupload = ref();
const back = () => {
    emit('updateDiv', 'income');
};


onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});




const nomineesave=()=>{



    relationship_c.value=selectedRelationship.value
    name_c.value=name.value
    dob_c.value=dob.value
    address_c.value=address.value

    visible.value=false
    skip.value=false
    nomineescard.value=true
}

const handleButtonClick=()=>{
    isAnimating.value = true;
    setTimeout(() => {
        isAnimating.value = false;
        buttonText.value = "Continue";
        emit('updateDiv', 'submission','2');
    }, 2000); // Adjust the duration as needed
};
</script>
<style>
.p-dialog-header{
    padding: 1% !important;
}
</style>