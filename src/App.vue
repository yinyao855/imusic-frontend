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
  },
  {
    name: '泡沫',
    singer: '邓紫棋',
    cover: './泡沫.webp',
    source: './泡沫.mp3'
  }
]

const lyrics = `
[00:00.60]关淑怡 - 难得有情人
[00:01.60]词：向雪怀
[00:02.60]曲：卢东尼
[00:29.74]如早春初醒 催促我的心
[00:34.95]将不可再等
[00:39.00]含情待放那岁月
[00:42.06]空出了痴心 令人动心
[00:49.57]幸福的光阴 它不会偏心
[00:54.77]将分给每颗心
[00:58.73]情缘亦远亦近 将交错一生
[01:04.39]情侣爱得更甚
[01:09.65]甜蜜地与爱人 风里飞奔
[01:14.25]高声欢呼你有情 不枉这生
[01:19.25]一声你愿意 一声我愿意
[01:24.50]惊天爱再没遗憾
[01:29.50]明月雾里照人 相爱相亲
[01:34.40]让对对的恋人 增添性感
[01:39.41]一些恋爱变恨
[01:41.56]更多恋爱故事动人
[01:44.01]划上了丝丝美感
[02:08.84]幸福的光阴 它不会偏心
[02:14.04]将分给每颗心
[02:18.05]情缘亦远亦近 将交错一生
[02:23.55]情侣爱得更甚
[02:28.90]甜蜜地与爱人 风里飞奔
[02:33.60]高声欢呼你有情 不枉这生
[02:38.55]一声你愿意 一声我愿意
[02:43.70]惊天爱再没遗憾
[02:48.71]明月雾里照人 相爱相亲
[02:53.71]让对对的恋人 增添性感
[02:58.61]一些恋爱变恨
[03:00.71]更多恋爱故事动人
[03:03.28]划上了丝丝美感
[03:08.43]一些恋爱变恨
[03:10.63]更多恋爱故事动人
[03:13.13]划上了丝丝美感
`;

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
  <Music_Play v-if="isfull" class="fixed top-0 left-0 w-full" @fullsize="changesize" :source="currentMusic.source"
  :name="currentMusic.name" :singer="currentMusic.singer" :cover="currentMusic.cover" :lrcContent="lyrics"></Music_Play>
</template>

<style>
#app{
  height: 100vh;
}
</style>

