<template>
    <!-- 上传按钮 -->
    <div class="flex flex-col items-center justify-center h-1/3">
        <label for="file-upload" class="flex flex-col items-center justify-center w-48 h-48 bg-slate-100 rounded-full shadow-md cursor-pointer">
        <svg xmlns="http://www.w3.org/2000/svg" class="w-12 h-12 text-slate-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6"></path>
        </svg>
        <span class="mt-2 text-sm font-semibold text-slate-500">Upload</span>
        </label>
        <input id="file-upload" type="file" class="hidden" @change="handleFileChange" />
    </div>
    <!-- 文件信息 -->
    <div class="flex flex-col items-center justify-center bg-green-300 h-32">
        <div class="text-sm font-semibold">File Name: {{ name }}</div>
        <div class="text-sm font-semibold">File Size: {{ size }} bytes</div>
    </div>
</template>
  
<script setup>
import { ref } from 'vue';
const flag=ref(false);

const file = ref(null);
// const isShow = ref(false);
const name = ref('');
const size = ref(0);

const handleFileChange = (e) => {
file.value = e.target.files[0];
// isShow.value = true;
flag.value=true;
console.log(file.value);
if (file.value){
name.value = file.value.name;
size.value = file.value.size;
}
}
</script>
  