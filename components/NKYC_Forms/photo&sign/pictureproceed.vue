<template>
    <div class="primary_color" >
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <logo style="width: 50px; height: 50px;"/>
            <profile/>
        </div>
        <div class="flex justify-between  p-2 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-4 px-2 p-1">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                   Looking good, Client
                </p>

                <p class="text-md mt-3 text-gray-500 font-normal leading-6">
                    Just a few more steps and you're done.
                </p>

                <div class="w-full  p-1 flex justify-center mt-3 h-64"  >
                 
                        <img v-if="props.data" :src="props.data" class="rounded-xl w-full hei"  alt="Base64 Image" />
                     
                   
                </div>
               

                

            </div>

            <div class="w-full">
                <p @click="retake" class="text-center cursor-pointer font-medium text-blue-600 py-3 mt-1 text-xl">
                    Retake 
                </p>
              <div class="w-full flex gap-2">
                <Button @click="retake()" class="primary_color cursor-pointer border-0 text-white w-1/6 dark:bg-slate-900">
                <i class="pi pi-angle-left text-3xl dark:text-white"></i>
            </Button>
                <Button type="button" @click="handleButtonClick"
                    class=" primary_color wave-btn text-white w-5/6 py-4 text-xl border-0  ">
                    {{ buttonText }}
                    <span v-if="isAnimating" class="wave"></span>
                </Button>
              </div>
               
            </div>


        </div>

    </div>

   



   
</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import { ref, onMounted, onBeforeUnmount } from 'vue';
const isAnimating = ref(false);
const buttonText = ref("Next");
const props = defineProps({
    data: {
        type: String,
        default: () => ({}),
    },
});

console.log(props.data)
const deviceHeight = ref(0);

onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});
const emit = defineEmits(['updateDiv']);
const retake = () => {
    emit('updateDiv', 'takephoto');
}



const handleButtonClick = () => {
 isAnimating.value = true;
    setTimeout(() => {
      isAnimating.value = false;
      emit('updateDiv', 'signature');
    }, 800); 
};









</script>
<style>

</style>