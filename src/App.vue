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

//歌单
const musicList = [
  {
    name: '难得有情人',
    singer: '关淑怡',
    cover: './难得有情人.png',
    source: './难得有情人.mp3'
  },
  {
    name: '天下',
    singer: '张杰',
    cover: './天下.webp',
    source: './天下.mp3'
  },
  {
    name: '喜帖街',
    singer: '谢安琪',
    cover: './喜帖街.webp',
    source: './喜帖街.mp3'
  },
  {
    name: '少女的祈祷',
    singer: '杨千嬅',
    cover: './少女的祈祷.webp',
    source: './少女的祈祷.mp3'
  }
]

//当前播放歌曲
const currentMusic = ref(musicList[0]);
let index = 0;

//下一首
function nextSong(){
  const length = musicList.length;
  index = (index + 1) % length;
  currentMusic.value = musicList[index];
}

//上一首
function backSong(){
  const length = musicList.length;
  index = (index - 1 + length) % length;
  currentMusic.value = musicList[index];
}
</script>

<template>
  <Upload></Upload>
  <!-- <Test></Test> -->
  <!-- <Progress></Progress> -->
  <MusicPlayer v-if="!isfull" :source="currentMusic.source" :name="currentMusic.name" 
  :singer="currentMusic.singer" :cover="currentMusic.cover" 
  @fullsize="changesize" @back="backSong" @next="nextSong"></MusicPlayer>
  <!-- <MusicPlayer source="./天下-张杰.128.mp3" name="天下" singer="张杰" cover="./天下.png"></MusicPlayer> -->
  <Music_Play v-if="isfull" class="fixed top-0 left-0 w-full" @fullsize="changesize"></Music_Play>
</template>

<style>
#app{
  height: 100vh;
}
</style>

