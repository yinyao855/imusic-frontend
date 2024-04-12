<template>
    <div class="progress-bar" ref="progressBar" @mousedown="startDrag">
      <div class="progress" ref="progress"></div>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    setup() {
      const progressBar = ref(null);
      const progress = ref(null);
      let isDragging = false;
  
      const startDrag = (e) => {
        isDragging = true;
        updateProgress(e);
      };
  
      const updateProgress = (e) => {
        if (!isDragging) return;
  
        const progressBarRect = progressBar.value.getBoundingClientRect();
        const mouseX = e.clientX - progressBarRect.left;
        const progressWidth = Math.min(progressBarRect.width, Math.max(0, mouseX));
        const percentage = (progressWidth / progressBarRect.width) * 100;
        progress.value.style.width = percentage + '%';
      };
  
      const endDrag = () => {
        isDragging = false;
      };
  
      // 添加事件监听器
      document.addEventListener('mousemove', updateProgress);
      document.addEventListener('mouseup', endDrag);
  
      // 在组件卸载时移除事件监听器，以避免内存泄漏
      const cleanup = () => {
        document.removeEventListener('mousemove', updateProgress);
        document.removeEventListener('mouseup', endDrag);
      };
  
      return { progressBar, progress, startDrag, cleanup };
    },
  
    beforeUnmount() {
      this.cleanup();
    }
  };
  </script>
  
  <style scoped>
  .progress-bar {
    width: 100%;
    height: 10px;
    background-color: #ccc;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .progress {
    height: 100%;
    background-color: #007bff;
    border-radius: 5px;
  }
  </style>
  