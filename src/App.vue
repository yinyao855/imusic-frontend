<script setup>
import MusicPlayer from "./components/MusicPlayer.vue";
import Upload from "./components/Upload.vue";
import {ref} from "vue";
import MusicTest from "./components/MusicTest.vue";
import {musicList} from "./js/lyrics.js";
import lyrics from "./js/lyrics.js";
import {gradient} from "./js/lyrics.js";

const isShow = ref(false);

const curMusicIndex = ref(0)

const playMusicByChoice = (index) =>{
  isShow.value = true;
  console.log("选择的歌曲"+index);
  curMusicIndex.value = index;
}

const close = () => {
  isShow.value = false;
};
</script>

<template>
<!--  <Upload></Upload>-->
  <MusicTest :musicList="musicList" @playMusic="playMusicByChoice"></MusicTest>
  <button @click="close" class="fixed top-14 right-14 btn btn-error mx-auto my-auto btn-outline">关闭播放器</button>

  <MusicPlayer v-if="isShow"
               v-model:curIndex="curMusicIndex"
               :musicList="musicList"
               :gradient="gradient"
               :lyrics="lyrics"
  ></MusicPlayer>
</template>

<style scoped>
</style>