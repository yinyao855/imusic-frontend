<script setup>
import MusicPlayer from './components/MusicPlayer.vue';
import Upload from './components/Upload.vue';
import Test from './components/Test.vue';
import Progress from './components/Progress.vue';
</script>

<template>
  <Upload></Upload>
  <!-- <Test></Test> -->
  <!-- <Progress></Progress> -->
  <MusicPlayer source="./难得有情人.mp3" name="难得有情人" singer="关淑怡" cover="./cover.png"></MusicPlayer>
</template>
