
<template>
    <div class="w-full">
       
        <img @click="visible = true" v-if="src" :src="src" alt="Image" class="shadow-md rounded-xl w-full mb-1 h-20" style="filter: grayscale(100%)" />
        <FileUpload mode="basic" @select="onFileSelect" chooseLabel="Bank proof"  customUpload auto severity="secondary" class=" p-button-outlined w-full" />
      
    </div>

    <Dialog v-model:visible="visible" modal header="View" :style="{ width: '25rem' }">
        <img v-if="src" :src="src" alt="Image" class="shadow-md rounded-xl w-full mb-1" style="filter: grayscale(100%)" />

</Dialog>
</template>

<script setup>
import { ref } from "vue";
const emit = defineEmits(["update:src"]);
const src = ref(null);
const visible = ref(false);
function onFileSelect(event) {
    const file = event.files[0];
    const reader = new FileReader();

    reader.onload = async (e) => {
        src.value = e.target.result;
        emit("update:src", src.value); 
    };

    reader.readAsDataURL(file);
}
</script>
