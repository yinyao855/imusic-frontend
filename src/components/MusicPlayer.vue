<template>
  <!-- 音乐播放 -->
  <audio :src="source" class="hidden" ref="audioPlayer" @timeupdate="updateTime" controls></audio>

  <!-- 缩小后的音乐播放器 -->
  <transition name="player-transition">
    <div v-if="isMinimized" class="fixed bottom-6 left-6 w-32 h-32 rounded-full bg-red-100 animate-spin1"
      @click="expandPlayer">
      <img :src="cover" alt="Album Art" class="h-32 w-32 rounded-full">
    </div>
  </transition>

  <transition name="player-transiton1">
    <div class="fixed bottom-0 w-full h-36" v-if="!isMinimized">
      <div class="music-player-container h-28 mx-3 my-2 bg-slate-50 rounded-md shadow-lg flex">
        <!-- 专辑封面 -->
        <div class="rounded h-24 w-24 my-auto ml-4">
          <img :src="cover" alt="Album Art" class="h-24 w-24 rounded">
        </div>
        <!-- 歌曲信息 -->
        <div class="flex flex-col ml-4 my-auto">
          <span class="text-lg font-semibold">{{ name }}</span>
          <span class="text-sm font-light">{{ singer }}</span>
        </div>
        <!-- 播放控制 -->
        <div class="flex flex-col ml-auto my-auto mr-4 w-2/3 h-4/5">
          <div class="flex h-2/3 justify-around">
            <!-- <button class="w-10 h-10 bg-slate-500 rounded-full"></button> -->
            <div class="w-4/5 justify-around">
              <div class="w-12 h-12 bg-slate-100 rounded-full my-auto" @click="togglePlay">
              <svg class="w-12 h-12" v-if="!isPlaying" viewBox="0 0 48 48" fill="none"
                xmlns="http://www.w3.org/2000/svg">
                <path d="M15 24V11.8756L25.5 17.9378L36 24L25.5 30.0622L15 36.1244V24Z" fill="none" stroke="#333"
                  stroke-width="2" stroke-linejoin="round" />
              </svg>
              <svg class="w-12 h-12" v-else viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M16 12V36" stroke="#333" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                <path d="M32 12V36" stroke="#333" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
              </svg>
              </div>
            </div>
            <button class="btn btn-outline btn-primary btn-sm my-auto ml-2" @click="minimizePlayer">下载</button>
            <button class="btn btn-outline btn-info btn-sm my-auto ml-2" @click="minimizePlayer">缩小</button>
            <button class="btn btn-outline btn-secondary btn-sm my-auto ml-2" @click="minimizePlayer">全屏</button>
          </div>
          <!-- 进度条 -->
          <div class="flex mt-2">
            <input type="range" class="w-full ml-1 range range-accent range-xs" min="0" :max="durationInSeconds" v-model="currentTimeInSeconds"
              @input="seek" />
          </div>
          <div class="flex justify-between mt-1">
            <span class="text-xs font-light">{{ currentTime }}</span>
            <span class="text-xs font-light text-right">{{ duration }}</span>
          </div>
        </div>
      </div>
    </div>
  </transition>

</template>

<script setup>
import { ref } from 'vue';
import { defineProps, watch } from 'vue';

const props = defineProps({
  cover: String,
  source: String,
  name: String,
  singer: String,
});

const isPlaying = ref(false);
const source = ref(props.source);
const name = ref(props.name);
const singer = ref(props.singer);
const currentTime = ref('0:00');
const duration = ref('0:00');

const durationInSeconds = ref(0);
const currentTimeInSeconds = ref(0);

const audioPlayer = ref(null);

const isMinimized = ref(false);

console.log(source.value);

const togglePlay = () => {
  if (isPlaying.value) {
    audioPlayer.value.pause();
  } else {
    audioPlayer.value.play();
  }
  isPlaying.value = !isPlaying.value;
};

const updateTime = () => {
  const audio = audioPlayer.value;
  const minutes = Math.floor(audio.currentTime / 60);
  const seconds = Math.floor(audio.currentTime % 60);
  currentTime.value = `${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;
  duration.value = `${Math.floor(audio.duration / 60)}:${Math.floor(audio.duration % 60)}`;
  currentTimeInSeconds.value = audio.currentTime;
  durationInSeconds.value = audio.duration;
};

const seek = () => {
  if (audioPlayer.value) {
    audioPlayer.value.currentTime = currentTimeInSeconds.value;
  }
};

function minimizePlayer() {
  isMinimized.value = true;
}

function expandPlayer() {
  isMinimized.value = false;
}
</script>

<style scoped>
.music-player-container {
  /* 设置背景图片填充方式 */
  background-size: cover;
  /* 设置背景图片的位置 */
  background-position: center;
  /* 使用 backdrop-filter 实现背景模糊效果，同时保持内部内容清晰 */
  backdrop-filter: blur(30px);
  /* 设置背景图片透明度 */
}

/* 过渡效果 */
.player-transition-enter-active,
.player-transition-leave-active {
  transition: all 0.5s ease;
}

.player-transition-enter,
.player-transition-leave-to {
  opacity: 0;
  transform: scale(0);
}

/* 过渡效果 */
.player-transition1-enter-active,
.player-transition1-leave-active {
  transition: all 3s ease;
}
.player-transition1-enter,
.player-transition1-leave-to {
  opacity: 0;
  transform: translateY(100%); /* 初始时从下方移动进入或离开 */
}

.player-transition1-enter-active,
.player-transition1-leave-active {
  transition: all 1s ease;
}
.player-transition1-enter,
.player-transition1-leave-to {
  opacity: 1;
  transform: translateY(-10); /* 从下方移动到正常位置 */
}


@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.animate-spin1 {
  animation: spin 4s linear infinite;
}

.animate-spin1:hover {
  animation-play-state: paused;
  /* transform: scale(1.1);
    transition-duration: 0.5s; */
}
</style>