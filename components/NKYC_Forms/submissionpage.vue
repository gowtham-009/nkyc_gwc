<template>
    <div>
        <div class="w-full bg-blue-50 dark:bg-black">
            <div class="w-full p-2 " :style="{ height: deviceHeight * 0.05 + 'px' }">
                <div class="w-full flex justify-between">
                    <logo style="width: 50px; height: 50px;" />
                    <profile />
                </div>
                <div class="w-full flex justify-center mt-1">
                    <!-- something -->
                </div>
            </div>
            <div class="w-full p-2  flex flex-col justify-between" :style="{ height: deviceHeight * 0.95 + 'px' }">
                <div class="w-full p-1 px-2">
                    <div class="w-full" v-if="completedbox">
                        <div class="w-full px-4 mt-1">
                            <div v-for="(step, index) in filteredSteps" :key="index"
                                class="w-full flex items-center gap-5 mt-1">
                                <div
                                    class="p-2 px-2 flex justify-center items-center static w-10 h-10 bg-green-400 dark:bg-slate-900 rounded-full flex-shrink-0">
                                    <span><i class="pi pi-check text-white text-xl"></i></span>
                                </div>
                                <div class="p-1">
                                    <p class="text-lg font-medium text-blue-950 dark:text-gray-400">{{ step.title }}</p>
                                    <p class="text-sm font-normal text-gray-500">{{ step.description }}</p>
                                </div>
                            </div>

                        </div>
                    </div>

                    <div class="w-full" v-if="pendingbox">

                        <div class="w-full mt-2">
                            <p class="text-2xl text-left text-blue-600 font-medium">
                                Next Up...
                            </p>
                        </div>

                        <div class="w-full px-4 mt-2">
                            <div v-for="(step, index) in stepspending.slice(props.data)" :key="index"
                                class="w-full flex items-center gap-5 mt-1">
                                <div
                                    class="p-2 px-2 flex justify-center items-center w-10 h-10 bg-blue-200 dark:bg-slate-900 rounded-full flex-shrink-0">
                                    <span><i :class="`pi ${step.icon} text-blue-900 text-xl`"></i></span>
                                </div>
                                <div class="p-1">
                                    <p class="text-lg font-medium text-blue-950 dark:text-gray-400">{{ step.title }}</p>
                                    <p class="text-sm font-normal text-gray-500">{{ step.description }}</p>
                                </div>
                            </div>
                        </div>

                    </div>
                </div>
                <div class="w-full flex gap-2">
                    <Button @click="back()" class="primary_color cursor-pointer border-0 text-white w-1/6 dark:bg-slate-900">
                <i class="pi pi-angle-left text-3xl dark:text-white"></i>
            </Button>
                    <Button type="button" label="Continue" @click="handleButtonClick"
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
import { ref } from 'vue';
import ThemeSwitch from '~/components/darkmode/darkmode.vue';

const props = defineProps({
    data: {
        type: Object,
        default: () => ({}),
    },
});


const emit = defineEmits(['updateDiv']);

const buttonText = ref("Continue");
const isAnimating = ref(false);
const completedbox = ref(false);

const deviceHeight = ref(0);






const steps = [
    { title: "Complete e-KYC", description: "Keep your Aadhaar and PAN card handy" },
    { title: "Set up your profile", description: "Answer a few questions about yourself" },
    { title: "Link your bank a/c", description: "Set the primary account for your transactions" },
    { title: "Select your account", description: "Upload proofs, Trading segment, Brokerage details." },
    { title: "Confirm it's you", description: "Click a photo and submit your signature" },
    { title: "eSign and Login", description: "Sign your application and start investing" }
];


const pendingbox = ref(true);

const stepspending = [
    { icon: "pi-folder-open", title: "Complete e-KYC", description: "Keep your Aadhaar and PAN card handy" },
    { icon: "pi-user", title: "Set up your profile", description: "Answer a few questions about yourself" },
    { icon: "pi-credit-card", title: "Link your bank a/c", description: "Set the primary account for your transactions" },
    { icon: "pi-building-columns", title: "Select your account", description: "Upload proofs, Trading segment, Brokerage details." },
    { icon: "pi-verified", title: "Confirm it's you", description: "Click a photo and submit your signature" },
    { icon: "pi-pen-to-square", title: "eSign and Login", description: "Sign your application and start investing" }
];



onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });


});


if (props.data) {
    completedbox.value = true;
}


const filteredSteps = computed(() => steps.slice(0, props.data));
const handleButtonClick = () => {
    isAnimating.value = true;
    setTimeout(() => {
        isAnimating.value = false;
        if (props.data == 1) {
            emit('updateDiv', 'info');
        }
        else if (props.data == 2) {
            emit('updateDiv', 'bank1');
        }
        else if (props.data == 3) {
            emit('updateDiv', 'tradingsegment');
        }
        else if (props.data == 4) {
            emit('updateDiv', 'photosign1');
        }
        else if (props.data == 5) {
            emit('updateDiv', 'thankyou');
        }

    }, 800);
};


function back() {
    if (props.data == 1) {
        emit('updateDiv', 'parmanentaddress')
    }
    else if (props.data == 2) {
        emit('updateDiv', 'nominee')
    }
    else if (props.data == 3) {
        emit('updateDiv', 'bank1')
    }
    else if (props.data == 4) {
        emit('updateDiv', 'uploadproof')
    }

}
</script>
