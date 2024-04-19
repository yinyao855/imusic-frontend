<template>
  <div class="background">
    <button class="menu__icon" @click="unfoldmenu">
      <span></span>
      <span></span>
      <span></span>
    </button>
  </div>
</template>

<style scoped>
@import url("../css/menu_button.css");
</style>

<script setup>
import { defineEmits } from 'vue';
const emit = defineEmits(['unfoldmenu']);
const unfoldmenu = () => {
  emit("unfoldmenu");
};
</script>
