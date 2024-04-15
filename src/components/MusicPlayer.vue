<template>
    <audio
      :src="currentMusic.source"
      class="hidden"
      ref="audioPlayer"
      @timeupdate="updateTime"
      @ended="handleModeChange"
      controls
      autoplay
    ></audio>

    <div v-if="!isFull">
      <MusicPlayerView
        :key="1"
        :name="currentMusic.name"
        :singer="currentMusic.singer"
        :cover="currentMusic.cover"
        @fullsize="changeSize"
        @back="backSong"
        @next="nextSong"
        v-model:currentTime="currentTime"
        v-model:duration="duration"
        v-model:isPlaying="isPlaying"
        v-model:durationInSeconds="durationInSeconds"
        v-model:currentTimeInSeconds="currentTimeInSeconds"
        v-model:audioPlayer="audioPlayer"
        v-model:playerMode="playerMode"
        @togglePlay="togglePlay"
      >
      </MusicPlayerView>
    </div>

    <transition name="slide" appear>
      <div v-if="isFull" key="musicPlay" class="transition-container">
        <MusicPlayFullView
          class="fixed top-0 left-0 w-full"
          v-model:audioPlayer="audioPlayer"
          v-model:durationInSeconds="durationInSeconds"
          v-model:currentTime="currentTime"
          v-model:isPlaying="isPlaying"
          v-model:duration="duration"
          v-model:currentTimeInSeconds="currentTimeInSeconds"
          @fullsize="changeSize"
          :name="currentMusic.name"
          :singer="currentMusic.singer"
          :cover="currentMusic.cover"
          v-model:lyric="lyric"
          @update="updateTime"
          :sty="gradient[index]"
          @togglePlay="togglePlay"
          @back="backSong"
          @next="nextSong"
        ></MusicPlayFullView>
      </div>
    </transition>

</template>

<script setup>
import MusicPlayerView from "./MusicPlayerView.vue";
import MusicPlayFullView from "./MusicPlayerFullView.vue";
import { ref } from "vue";
//歌词
import lyrics from "../js/lyrics.js";
//背景
import { gradient } from "../js/lyrics.js";

const isFull = ref(false);

function changeSize() {
  isFull.value = !isFull.value;
}

//歌单
const musicList = [
  {
    name: "难得有情人",
    singer: "关淑怡",
    cover: "./难得有情人.png",
    source: "./难得有情人.mp3",
  },
  {
    name: "天下",
    singer: "张杰",
    cover: "./天下.webp",
    source: "./天下.mp3",
  },
  {
    name: "喜帖街",
    singer: "谢安琪",
    cover: "./喜帖街.webp",
    source: "./喜帖街.mp3",
  },
  {
    name: "少女的祈祷",
    singer: "杨千嬅",
    cover: "./少女的祈祷.webp",
    source: "./少女的祈祷.mp3",
  },
  {
    name: "泡沫",
    singer: "邓紫棋",
    cover: "./泡沫.webp",
    source: "./泡沫.mp3",
  },
  {
    name: "Something Just Like This",
    singer: "The Chain smokers,Coldplay",
    cover: "./Something Just Like This.webp",
    source: "./Something Just Like This.mp3",
  },
  {
    name: "海阔天空",
    singer: "Beyond",
    cover: "./海阔天空.jpg",
    source: "./海阔天空.mp3",
  },
];


const lyric = ref(Array);
lyric.value = parseLRC(lyrics[0]);

const currentMusic = ref(musicList[0]);
let index = 0;

const playerMode = ref(0)

//播放设置
function handleModeChange() {
  if (playerMode.value === 0){
    nextSong();
  }
  else if (playerMode.value === 1){
    audioPlayer.value.currentTime = 0;
    audioPlayer.value.play();
  }
  else {
    randomSong();
  }
}

//上一首
function backSong() {
  const length = musicList.length;
  index = (index - 1 + length) % length;
  currentMusic.value = musicList[index];
  lyric.value = parseLRC(lyrics[index]);
  isPlaying.value = true;
}

//下一首
function nextSong() {
  const length = musicList.length;
  index = (index + 1) % length;
  currentMusic.value = musicList[index];
  lyric.value = parseLRC(lyrics[index]);
  isPlaying.value = true;
}

function getRandomInt(max) {
  return Math.floor(Math.random() * max);
}

//随机选取
function randomSong() {
  const length = musicList.length;
  index = getRandomInt(length)
  currentMusic.value = musicList[index];
  lyric.value = parseLRC(lyrics[index]);
  isPlaying.value = true;
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
  const lines = lrc.split("\n");
  const lyrics = [];
  const timeRegex = /\[(\d{2}):(\d{2})\.(\d{2})](.*)/;

  lines.forEach((line) => {
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
const isPlaying = ref(true);

//当前播放时间和总时间
const currentTime = ref("0:00");
const duration = ref("0:00");
//当前播放时间和总时间（秒）
const durationInSeconds = ref(0);
const currentTimeInSeconds = ref(0);
const updateTime = () => {
  const audio = audioPlayer.value;
  let minutes = Math.floor(audio.currentTime / 60);
  let seconds = Math.floor(audio.currentTime % 60);
  currentTime.value = `${minutes}:${seconds < 10 ? "0" : ""}${seconds}`;
  minutes = Math.floor(audio.duration / 60);
  seconds = Math.floor(audio.duration % 60);
  duration.value = `${minutes}:${seconds < 10 ? "0" : ""}${seconds}`;
  currentTimeInSeconds.value = audio.currentTime;
  durationInSeconds.value = audio.duration;
};
</script>

<style>
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
