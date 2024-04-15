<script setup>
import MusicPlayer from "./components/MusicPlayer.vue";
import Upload from "./components/Upload.vue";
import {ref} from "vue";

const isShow = ref(false);

const begin = () => {
  isShow.value = true;
};
</script>

<template>
  <Upload></Upload>
  <div class="w-full flex">
    <button @click="begin" class="btn btn-info mx-auto my-auto btn-outline">开始</button>
  </div>

  <!-- <Test></Test> -->

  <MusicPlayer v-if="isShow"></MusicPlayer>
</template>

<style scoped>
#app {
  height: 100vh;
}
</style>