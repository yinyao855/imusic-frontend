<script setup>
import MusicPlayer from './components/MusicPlayer.vue';
import Upload from './components/Upload.vue';
import Test from './components/Test.vue';
import Progress from './components/Progress.vue';
import Music_Play from './components/Music_Play.vue';
import { ref } from 'vue';

const isfull = ref(false);

function changesize(){
  isfull.value = !isfull.value;
}
</script>

<template>
  <Upload></Upload>
  <!-- <Test></Test> -->
  <!-- <Progress></Progress> -->
  <MusicPlayer v-if="!isfull" source="./难得有情人.mp3" name="难得有情人" singer="关淑怡" cover="./cover.png" @fullsize="changesize"></MusicPlayer>
  <!-- <MusicPlayer source="./天下-张杰.128.mp3" name="天下" singer="张杰" cover="./天下.png"></MusicPlayer> -->
  <Music_Play v-if="isfull" class="fixed top-0 left-0 w-full" ></Music_Play>
</template>

<style>
#app{
  height: 100vh;
}
</style>

