<template>
  <Upload></Upload>
  <!-- <Test></Test> -->

  <!-- 音乐播放 -->
  <audio :src="currentMusic.source" class="hidden" ref="audioPlayer" @timeupdate="updateTime" controls></audio>

  <div v-if="!isfull">
    <MusicPlayer :key="1" :name="currentMusic.name" :singer="currentMusic.singer"
      :cover="currentMusic.cover" @fullsize="changesize" @back="backSong" @next="nextSong"
      v-model:currentTime="currentTime" v-model:duration="duration" v-model:isPlaying="isPlaying"
      v-model:durationInSeconds="durationInSeconds" v-model:currentTimeInSeconds="currentTimeInSeconds"
      v-model:audioPlayer="audioPlayer" @togglePlay="togglePlay">
    </MusicPlayer>
  </div>

  <transition name="slide" appear>
    <div v-if="isfull" key="musicPlay" class="transition-container">
      <Music_Play class="fixed top-0 left-0 w-full" v-model:currentTime="currentTime" v-model:isPlaying="isPlaying" v-model:duration="duration"
        v-model:durationInseconds="durationInSeconds" v-model:currentTimeInSeconds="currentTimeInSeconds" @fullsize="changesize" 
        :name="currentMusic.name" :singer="currentMusic.singer" :cover="currentMusic.cover" v-model:lyric="lyricsx" @update="updateTime"
        :sty="gradient[index]" @togglePlay="togglePlay"></Music_Play>

    </div>
  </transition>
</template>

<script setup>
import MusicPlayer from './components/MusicPlayer.vue';
import Upload from './components/Upload.vue';
import Test from './components/Test.vue';
import Progress from './components/Progress.vue';
import Music_Play from './components/Music_Play.vue';
import { ref } from 'vue';
//歌词
import lyrics from './js/lyrics';
//背景
import { gradient } from './js/lyrics';

const isfull = ref(false);

function changesize() {
  isfull.value = !isfull.value;
  // console.log("当前时间" + currenttime.value);
  // console.log("当前秒数" + currentduration.value);
  // console.log("是否播放" + isPlaying.value);
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
    source: './天下.mp3',
    color1: '#101010',
    color2: '#070707'
  },
  {
    name: '喜帖街',
    singer: '谢安琪',
    cover: './喜帖街.webp',
    source: './喜帖街.mp3',
    color1: '#423e3d',
    color2: '#595755'
  },
  {
    name: '少女的祈祷',
    singer: '杨千嬅',
    cover: './少女的祈祷.webp',
    source: './少女的祈祷.mp3',
    color1: '#f1d3ab',
    color2: '#c8c9a5'
  },
  {
    name: '泡沫',
    singer: '邓紫棋',
    cover: './泡沫.webp',
    source: './泡沫.mp3'
  }
]

let lrcContent = ref(lyrics[0]);

const lyricsx = ref(Array);
lyricsx.value = parseLRC(lyrics[0]);
console.log(lyricsx.value);
const currentMusic = ref(musicList[0]);
let index = 0;

//上一首
function backSong() {
  const length = musicList.length;
  index = (index - 1 + length) % length;
  currentMusic.value = musicList[index];
  lrcContent.value = lyrics[index];
  lyricsx.value = parseLRC(lrcContent.value);
  isPlaying.value = true;
  // audioPlayer.value.play();
}

//下一首
function nextSong() {
  const length = musicList.length;
  index = (index + 1) % length;
  currentMusic.value = musicList[index];
  lrcContent.value = lyrics[index];
  lyricsx.value = parseLRC(lrcContent.value);
  console.log(lyricsx.value);
  isPlaying.value = true;
  // audioPlayer.value.play();
}

const togglePlay = () => {
  if (isPlaying.value) {
    audioPlayer.value.pause();
  } else {
    audioPlayer.value.play();
  }
  isPlaying.value = !isPlaying.value;
};

function parseLRC(lrc) {
  const lines = lrc.split('\n');
  const lyrics = [];
  const timeRegex = /\[(\d{2}):(\d{2})\.(\d{2})\](.*)/;

  lines.forEach(line => {
    const match = timeRegex.exec(line);
    if (match) {
      const minute = parseInt(match[1]);
      const second = parseInt(match[2]);
      const millisecond = parseInt(match[3]);
      const timestamp = minute * 60 + second + millisecond / 1000;
      const text = match[4].trim();
      lyrics.push({ timestamp, text });
    }
  });
  return lyrics;
}


const audioPlayer = ref(null);

const isPlaying = ref(false);

//当前播放时间和总时间
const currentTime = ref('0:00');
const duration = ref('0:00');
//当前播放时间和总时间（秒）
const durationInSeconds = ref(0);
const currentTimeInSeconds = ref(0);

const updateTime = () => {
  const audio = audioPlayer.value;
  const minutes = Math.floor(audio.currentTime / 60);
  const seconds = Math.floor(audio.currentTime % 60);
  currentTime.value = `${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;
  duration.value = `${Math.floor(audio.duration / 60)}:${Math.floor(audio.duration % 60)}`;
  currentTimeInSeconds.value = audio.currentTime;
  durationInSeconds.value = audio.duration;
};
</script>

<style>
#app {
  height: 100vh;
}

.slide-leave-active {
  transition: transform 0.5s ease;
}

.slide-enter-active {
  transition: transform 0.5s ease;
}

.slide-enter-from,
.slide-leave-to {
  transform: translateX(-100%);
}

.slide-enter-to,
.slide-leave-from {
  transform: translateX(0);
}

.transition-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
