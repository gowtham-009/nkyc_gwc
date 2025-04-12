<template>
    <div class="w-full">
      
      <!-- Image Preview -->
      <img @click="visible = true"
        v-if="src && isImage"
        :src="src"
        alt="Uploaded Image"
        class="shadow-md rounded-xl w-full mb-1 h-20"
        style="filter: grayscale(100%)"
      />
  
      <!-- PDF Preview as link -->
      <a
        v-if="src && isPdf"
        :href="src"
        target="_blank"
        class="text-blue-500 underline"
      >
        View uploaded PDF
      </a>
  
      <!-- File Upload -->
      <FileUpload
        mode="basic"
        @select="onFileSelect"
        chooseLabel="Income proof"
        customUpload
        auto
        severity="secondary"
        class="p-button-outlined w-full"
        accept="image/*,application/pdf"
      />
    </div>

    <Dialog v-model:visible="visible" modal header="View" :style="{ width: '25rem' }">
        <img v-if="src" :src="src" alt="Image" class="shadow-md rounded-xl w-full mb-1" style="filter: grayscale(100%)" />

</Dialog>
  </template>
  
  <script setup>
import { ref } from "vue";

const emit = defineEmits(["update:src", "update:isImage", "update:isPdf"]);

const src = ref(null);
const isImage = ref(false);
const isPdf = ref(false);
const visible = ref(false);
function onFileSelect(event) {
  const file = event.files[0];
  const reader = new FileReader();

  const fileType = file.type;

  if (fileType.startsWith("image/")) {
    isImage.value = true;
    isPdf.value = false;

    reader.onload = (e) => {
      src.value = e.target.result;
      emit("update:src", src.value);
      emit("update:isImage", isImage.value);
      emit("update:isPdf", isPdf.value);
    };
    reader.readAsDataURL(file);
  } else if (fileType === "application/pdf") {
    isImage.value = false;
    isPdf.value = true;

    reader.onload = (e) => {
      src.value = e.target.result;
      emit("update:src", src.value);
      emit("update:isImage", isImage.value);
      emit("update:isPdf", isPdf.value);
    };
    reader.readAsDataURL(file);
  } else {
    isImage.value = false;
    isPdf.value = false;
    src.value = null;

    emit("update:src", null);
    emit("update:isImage", false);
    emit("update:isPdf", false);

    alert("Unsupported file type. Please upload an image or a PDF.");
  }
}
</script>

  