<template>
  <!-- 缩小后的音乐播放器 -->
  <Transition name="player-transition">
    <div v-if="isMinimized" class="fixed bottom-6 left-6 w-32 h-32 rounded-full bg-red-100 animate-spin1"
      @click="expandPlayer">
      <img :src="props.cover" alt="Album Art" class="h-32 w-32 rounded-full">
    </div>
  </Transition>

  <Transition name="slide-fade">
    <div class="fixed bottom-0 w-full h-36 bg-opacity-0" v-if="!isMinimized">
      <div class="music-player-container h-28 mx-3 my-2 bg-slate-50 rounded-md shadow-lg flex bg-opacity-100">
        <!-- 专辑封面 -->
        <div class="rounded h-24 w-24 my-auto ml-4">
          <img :src="props.cover" alt="Album Art" class="h-24 w-24 rounded">
        </div>
        <!-- 歌曲信息 -->
        <div class="flex flex-col ml-4 my-auto">
          <span class="text-lg font-semibold">{{ props.name }}</span>
          <span class="text-sm font-light">{{ props.singer }}</span>
        </div>
        <!-- 播放控制 -->
        <div class="flex flex-col ml-auto my-auto mr-4 w-1/2 h-4/5">
          <div class="flex h-2/3 justify-around w-1/2 mx-auto">
            <!--播放上一首-->
            <div class="tooltip my-auto" data-tip="上一首">
              <button class="btn glass btn-sm" @click="goBack">
                <svg width="28" height="28" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M34 36L22 24L34 12" stroke="#333" stroke-width="4" stroke-linecap="round"
                    stroke-linejoin="round" />
                  <path d="M14 12V36" stroke="#333" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
                </svg>
              </button>
            </div>
            <div class="tooltip my-auto" data-tip="播放与暂停">
              <button class="btn glass" @click="togglePlay">
                <svg v-if="!isPlaying" width="40" height="40" viewBox="0 0 48 48" fill="none"
                  xmlns="http://www.w3.org/2000/svg">
                  <path d="M15 24V11.8756L25.5 17.9378L36 24L25.5 30.0622L15 36.1244V24Z" fill="#333" stroke="#333"
                    stroke-width="4" stroke-linejoin="round" />
                </svg>
                <svg v-else width="40" height="40" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M16 12V36" stroke="#333" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
                  <path d="M32 12V36" stroke="#333" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
                </svg>
              </button>
            </div>
            <!--播放下一首-->
            <div class="tooltip my-auto" data-tip="下一首">
              <button class="btn glass btn-sm" @click="goNext">
                <svg width="28" height="28" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M14 12L26 24L14 36" stroke="#333" stroke-width="4" stroke-linecap="round"
                    stroke-linejoin="round" />
                  <path d="M34 12V36" stroke="#333" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
                </svg>
              </button>
            </div>
          </div>
          <!-- 进度条 -->
          <div class="flex mt-2">
            <input type="range" class="w-full ml-1 range range-accent range-xs" min="0" :max="durationInSeconds"
              v-model="currentTimeInSeconds" @input="seek" />
          </div>
          <div class="flex justify-between mt-1">
            <span class="text-xs font-light">{{ currentTime }}</span>
            <span class="text-xs font-light text-right">{{ duration }}</span>
          </div>
        </div>
        <!-- 其他控制 -->
        <div class="w-1/4 flex justify-around">
          <!--控制播放速度-->
          <div class="tooltip my-auto" data-tip="播放速度">
            <button class="btn glass btn-sm">
              <svg width="24" height="24" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path
                  d="M34.0234 6.68921C31.0764 4.97912 27.6525 4 24 4C12.9543 4 4 12.9543 4 24C4 35.0457 12.9543 44 24 44C35.0457 44 44 35.0457 44 24C44 20.3727 43.0344 16.9709 41.3461 14.0377"
                  stroke="#333" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
                <path
                  d="M31.9498 16.0503C31.9498 16.0503 28.5621 25.0948 27.0001 26.6569C25.438 28.219 22.9053 28.219 21.3432 26.6569C19.7811 25.0948 19.7811 22.5621 21.3432 21C22.9053 19.4379 31.9498 16.0503 31.9498 16.0503Z"
                  fill="none" stroke="#333" stroke-width="4" stroke-linejoin="round" />
              </svg>
            </button>
          </div>
          <!--控制播放方式-->
          <div class="tooltip my-auto" :data-tip="playerModeText">
            <button class="btn glass btn-sm" @click="changeMode">
              <svg v-if="playerMode === 0" width="24" height="24" viewBox="0 0 48 48" fill="none"
                xmlns="http://www.w3.org/2000/svg">
                <path
                  d="M43.8233 25.2305C43.7019 25.9889 43.5195 26.727 43.2814 27.4395C42.763 28.9914 41.9801 30.4222 40.9863 31.6785C38.4222 34.9201 34.454 37 30 37H16C9.39697 37 4 31.6785 4 25C4 18.3502 9.39624 13 16 13H44"
                  stroke="#333" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
                <path d="M38 7L44 13L38 19" stroke="#333" stroke-width="4" stroke-linecap="round"
                  stroke-linejoin="round" />
              </svg>
              <svg v-if="playerMode === 1" width="24" height="24" viewBox="0 0 48 48" fill="none"
                xmlns="http://www.w3.org/2000/svg">
                <path
                  d="M43.8233 25.2305C43.7019 25.9889 43.5195 26.727 43.2814 27.4395C42.763 28.9914 41.9801 30.4222 40.9863 31.6785C38.4222 34.9201 34.454 37 30 37H16C9.39697 37 4 31.6785 4 25C4 18.3502 9.39624 13 16 13H44"
                  stroke="#333" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
                <path d="M38 7L44 13L38 19" stroke="#333" stroke-width="4" stroke-linecap="round"
                  stroke-linejoin="round" />
                <path d="M24 19V31" stroke="#333" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
                <path d="M24 19L21 22L19.5 23.5" stroke="#333" stroke-width="4" stroke-linecap="round"
                  stroke-linejoin="round" />
              </svg>
              <svg v-if="playerMode === 2" width="24" height="24" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M4 25C4 18.3502 9.39624 13 16 13H44" stroke="#333" stroke-width="4" stroke-linecap="round"
                  stroke-linejoin="round" />
                <path d="M38 7L44 13L38 19" stroke="#333" stroke-width="4" stroke-linecap="round"
                  stroke-linejoin="round" />
                <path d="M44 23C44 29.6498 38.6038 35 32 35H4" stroke="#333" stroke-width="4" stroke-linecap="round"
                  stroke-linejoin="round" />
                <path d="M10 41L4 35L10 29" stroke="#333" stroke-width="4" stroke-linecap="round"
                  stroke-linejoin="round" />
              </svg>
            </button>
          </div>
          <!--控制音量-->
          <div class="my-auto flex">
            <button class="btn glass my-auto btn-sm">
              <svg width="24" height="24" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M24 3.99976V43.9998" stroke="#333" stroke-width="4" stroke-linecap="round" />
                <path d="M34 11.9998V35.9998" stroke="#333" stroke-width="4" stroke-linecap="round" />
                <path d="M4 17.9998V29.9998" stroke="#333" stroke-width="4" stroke-linecap="round" />
                <path d="M44 17.9998V29.9998" stroke="#333" stroke-width="4" stroke-linecap="round" />
                <path d="M14 11.9998V35.9998" stroke="#333" stroke-width="4" stroke-linecap="round" />
              </svg>
            </button>
            <input type="range" min="0" max="100" value="40" class="range range-xs my-auto" v-model="volume"
              @input="changeVolume" />
          </div>
          <!--缩小播放器-->
          <div class="tooltip my-auto" data-tip="最小化">
            <button class="btn glass btn-sm" @click="minimizePlayer">
              <svg width="24" height="24" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M27 9V21H39" stroke="#333" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
                <path d="M21 39V27H9" stroke="#333" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
                <path d="M27 21L42 6" stroke="#333" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
                <path d="M21 27L6 42" stroke="#333" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
              </svg>
            </button>
          </div>
          <!--全屏播放器-->
          <div class="tooltip my-auto" data-tip="全屏显示">
            <button class="btn glass btn-sm" @click="fullSize">
              <svg width="24" height="24" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M22 42H6V26" stroke="#333" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
                <path d="M26 6H42V22" stroke="#333" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
              </svg>
            </button>
          </div>

        </div>
      </div>
    </div>
  </Transition>

</template>

<script setup>
import { ref } from 'vue';
import { defineProps, defineModel } from 'vue';

const props = defineProps({
  cover: String,
  name: String,
  singer: String,
});

const emit = defineEmits([
  'fullsize',
  'back',
  'next',
  'togglePlay',
]);

//是否正在播放
const isPlaying = defineModel("isPlaying");
//当前播放时间和总时间
const currentTime = defineModel("currentTime");
const duration = defineModel("duration");
//当前播放时间和总时间（秒）
const durationInSeconds = defineModel("durationInSeconds");
const currentTimeInSeconds = defineModel("currentTimeInSeconds");
//音频播放器对象
const audioPlayer = defineModel("audioPlayer");
//定义播放模式, 0为列表循环，1为单曲循环，2为随机播放
const playerMode = defineModel("playerMode");
const playerModeText = ref('列表循环');
const modeList = ['列表循环', '单曲循环', '随机播放'];
//是否最小化
const isMinimized = ref(false);
//音量
const volume = ref(40);

//改变音量
const changeVolume = () => {
  audioPlayer.value.volume = volume.value / 100;
}

//播放上一首
const goBack = () => {
  emit('back');
  console.log('back');
}

//播放下一首
const goNext = () => {
  emit('next');
  console.log('next');
}

//改变播放模式
const changeMode = () => {
  const newMode = (playerMode.value + 1) % 3;
  // console.log(newMode);
  playerModeText.value = modeList[newMode];
  playerMode.value = newMode;
}

const togglePlay = () => {
  emit('togglePlay');
};

const seek = () => {
  if (audioPlayer.value) {
    audioPlayer.value.currentTime = currentTimeInSeconds.value;
    console.log(currentTimeInSeconds.value);
  }
};

function minimizePlayer() {
  isMinimized.value = true;
}

function expandPlayer() {
  isMinimized.value = false;
}

//全屏显示
function fullSize() {
  emit('fullsize');
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

/* 最小化播放器的过渡效果 */
.player-transition-enter-active,
.player-transition-leave-active {
  transition: all 0.8s ease-in-out;
}

.player-transition-enter-from,
.player-transition-leave-to {
  opacity: 0;
  transform: scale(0);
}

/* 默认播放器的过渡效果 */
.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateY(50px);
  opacity: 0;
}

/* 旋转动画 */
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