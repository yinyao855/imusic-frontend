<template>
  <div class="outcontainer" :style="sty">
    <div class="col1">
      <div class="button_div">
        <buttonchangesize style="display: block" @fullsize="changesize"></buttonchangesize>
      </div>
      <div class="card">
        <label for="uploadx">
          <!-- <input type="file" @change="handleFileChange" id="uploadx"
                 style="opacity: 0; position: absolute; left: -9999px;"> -->
          <!-- <button class="card__btn card__btn-menu">
            <svg fill="none" height="18" viewBox="0 0 24 18" width="24" xmlns="http://www.w3.org/2000/svg">
              <path d="m0 0h24v3h-12-12zm0 7.5h24v3h-24zm0 7.5h24v3h-24z" fill="#fff"></path>
            </svg>
          </button> -->
          <div class="card__img">
            <!-- <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 128 128" class="content stop">
              <circle r="60" fill="#ffd8c9" cy="64" cx="64"></circle>
              <circle r="48" opacity=".3" fill="#fff" cy="64" cx="64"></circle>
              <path fill="#393c54"
                    d="m64 14a31 31 0 0 1 31 31v41.07a9.93 9.93 0 0 1 -9.93 9.93h-42.14a9.93 9.93 0 0 1 -9.93-9.93v-41.07a31 31 0 0 1 31-31z"></path>
              <circle r="7" fill="#fbc0aa" cy="60" cx="89"></circle>
              <path fill="#00adfe"
                    d="m64 124a59.7 59.7 0 0 0 34.7-11.07l-3.33-10.29a10 10 0 0 0 -9.37-6.64h-43.95a10 10 0 0 0 -9.42 6.64l-3.33 10.29a59.7 59.7 0 0 0 34.7 11.07z"></path>
              <path fill="#ff8475" d="m46.54 121.45a59.93 59.93 0 0 0 34.92 0l-2.46-25.45h-30z"></path>
              <path fill="#f85565" d="m48.13 105h31.74l-.39-4h-30.96z"></path>
              <path fill="#ffd8c9" d="m76 96a12 12 0 0 1 -24 0z"></path>
              <path stroke-width="14" stroke-linejoin="round" stroke-linecap="round" stroke="#fbc0aa" fill="none"
                    d="m64 83v12"></path>
              <circle r="7" fill="#fbc0aa" cy="60" cx="39"></circle>
              <path fill="#ffd8c9"
                    d="m64 90a25 25 0 0 1 -25-25v-16.48a25 25 0 1 1 50 0v16.48a25 25 0 0 1 -25 25z"></path>
              <path stroke-width="5" stroke-linejoin="round" stroke-linecap="round" stroke="#fbc0aa" fill="none"
                    d="m64 64.75v6.5"></path>
              <path fill="#515570"
                    d="m64.83 18.35a27.51 27.51 0 0 0 -28.32 27.47v4.76a2 2 0 0 0 2 2h.58a1 1 0 0 0 .86-.49l4.05-7.09 2.48 4.13a1 1 0 0 0 1.71 0l2.48-4.13 2.47 4.13a1 1 0 0 0 1.72 0l2.47-4.13 2.48 4.13a1 1 0 0 0 1.71 0l2.48-4.13 2.48 4.13a1 1 0 0 0 1.71 0l2.48-4.13 2.47 4.13a1 1 0 0 0 1.72 0l2.47-4.13 2.48 4.13a1 1 0 0 0 1.71 0l2.48-4.13 4 7.09a1 1 0 0 0 .86.49h.58a2 2 0 0 0 2-2v-4.18c.05-14.95-11.66-27.61-26.61-28.05z"></path>
              <path fill="#f85565" d="m47.35 113h33.29l-.38-4h-32.52z"></path>
              <path fill="#f85565" d="m46.58 121h34.84l-.39-4h-34.06z"></path>
              <path opacity=".7" fill="#ff8475"
                    d="m58.52 79.39c0-.84 11-.84 11 0 0 1.79-2.45 3.25-5.48 3.25s-5.52-1.46-5.52-3.25z"></path>
              <path opacity=".7" fill="#f85565"
                    d="m69.48 79.29c0 .78-11 .78-11 0 .04-1.79 2.52-3.29 5.52-3.29s5.48 1.5 5.48 3.29z"></path>
              <circle r="3" fill="#515570" cy="58.75" cx="76.25"></circle>
              <path stroke-linejoin="round" stroke-linecap="round" stroke="#515570" fill="none"
                    d="m70.75 59.84a6.61 6.61 0 0 1 11.5-1.31"></path>
              <path
                  style="fill:none;stroke-linecap:round;stroke-linejoin:round;stroke:#515570;stroke-width:2;opacity:.2"
                  d="m72.11 51.46 5.68-.4a4.62 4.62 0 0 1 4.21 2.1l.77 1.21"></path>
              <circle r="3" fill="#515570" cy="58.75" cx="51.75"></circle>
              <g stroke-linecap="round" fill="none">
                <path stroke-linejoin="round" stroke="#515570" d="m57.25 59.84a6.61 6.61 0 0 0 -11.5-1.31"></path>
                <path stroke-width="2" stroke-linejoin="round" stroke="#515570" opacity=".2"
                      d="m55.89 51.45-5.68-.39a4.59 4.59 0 0 0 -4.21 2.11l-.77 1.21"></path>
                <path stroke-miterlimit="10" stroke="#f85565"
                      d="m57.25 78.76a17.4 17.4 0 0 0 6.75 1.12 17.4 17.4 0 0 0 6.75-1.12"></path>
              </g>
            </svg> -->
            <img :src="props.cover" class="content stop rounded-full w-[243px] h-[243px]">
          </div>
          <div class="card__title" style="font-weight: bolder !important;">{{ props.name }}</div>
          <div class="card__subtitle">{{ props.singer }}</div>
          <div class="card__wrapper">
            <div class="card__time card__time-passed">{{ currenttime }}</div>
            <div class="card__timeline">
              <input type="range" min="0" :max="maxlength" v-model="currentduration" @input="handleChange">
              <!--              <progress v-model="currentduration" :max="maxlength" @input="handleChange"></progress>-->
            </div>
            <div class="card__time card__time-left">{{ durationtime }}</div>
          </div>
        </label>
        <div class="card__wrapper">
          <button class="card__btn" @click="restart">
            <svg fill="none" height="12" viewBox="0 0 20 12" width="20" xmlns="http://www.w3.org/2000/svg"
                 xmlns:xlink="http://www.w3.org/1999/xlink">
              <clipPath id="a">
                <path d="m0 0h20v12h-20z"></path>
              </clipPath>
              <g>
                <path
                    d="m17 1c0-.265216-.1054-.51957-.2929-.707107-.1875-.187536-.4419-.292893-.7071-.292893h-8v2h7v5h-3l3.969 5 4.031-5h-3zm-14 10c0 .2652.10536.5196.29289.7071.18754.1875.44189.2929.70711.2929h8v-2h-7v-5h3l-4-5-4 5h3z"
                    fill="#fff"></path>
              </g>
            </svg>
          </button>
          <button class="card__btn">
            <svg width="23" height="16" viewBox="0 0 23 16" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M11.5 8V0L0 8L11.5 16V8ZM23 0L11.5 8L23 16V0Z" fill="#fff"></path>
            </svg>
          </button>
          <button class="card__btn card__btn-play" @click="togglePlay">
            <svg fill="#000" height="22" viewBox="0 0 18 22" width="18" xmlns="http://www.w3.org/2000/svg"
                 v-if="!isPlaying">
              <path d="m0 0v22l18-11z" fill="#000"></path>
            </svg>
            <svg class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" width="20"
                 fill="#fff"
                 height="20" v-if="isPlaying">
              <path
                  d="M128 106.858667C128 94.976 137.621333 85.333333 149.12 85.333333h85.76c11.648 0 21.12 9.6 21.12 21.525334V917.12c0 11.882667-9.621333 21.525333-21.12 21.525333H149.12A21.290667 21.290667 0 0 1 128 917.141333V106.88z m640 0c0-11.882667 9.621333-21.525333 21.12-21.525334h85.76c11.648 0 21.12 9.6 21.12 21.525334V917.12c0 11.882667-9.621333 21.525333-21.12 21.525333h-85.76a21.290667 21.290667 0 0 1-21.12-21.525333V106.88z"
                  fill="#3D3D3D"></path>
            </svg>
          </button>
          <button class="card__btn">
            <svg width="23" height="16" viewBox="0 0 23 16" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M11.5 8V0L23 8L11.5 16V8ZM0 0L11.5 8L0 16V0Z" fill="#fff"></path>
            </svg>
          </button>
          <button class="card__btn">
            <svg fill="#fff" height="20" viewBox="0 0 20 20" width="20" xmlns="http://www.w3.org/2000/svg"
                 xmlns:xlink="http://www.w3.org/1999/xlink">
              <clipPath id="a">
                <path d="m0 .5h20v19h-20z"></path>
              </clipPath>
              <g fill="#fff">
                <path
                    d="m15 14.5h-1.559l-9.7-10.673c-.09376-.10305-.20802-.18536-.33545-.24168-.12744-.05631-.26523-.08537-.40455-.08532h-3.001v2h2.559l4.09 4.5-4.09 4.501h-2.559v2h3.001c.13932 0 .27711-.029.40455-.0853.12743-.0563.24169-.1387.33545-.2417l4.259-4.687 4.259 4.686c.0938.103.208.1854.3355.2417.1274.0563.2652.0853.4045.0853h2.001v3l5-4-5-4z"></path>
                <path
                    d="m13.4406 5.5h1.559v3l5-3.938-5-4.062v3h-2.001c-.1393-.00005-.2771.02901-.4045.08532-.1275.05632-.2417.13863-.3355.24168l-3.36798 3.707 1.47998 1.346z"></path>
              </g>
            </svg>
          </button>
        </div>
        <audio ref="audioPlayer" :src="props.source" @timeupdate="getCurrentTime" @loadedmetadata="getDuration"></audio>
      </div>
    </div>
    <div class="col2">
      

      <div style="width:100%;  display:flex; align-items: center; justify-content: center; margin: 0;" class="lyricclass">
        <ul style="width:100%;">
    <span class="box" v-for="(item, index) in lyricsshow" :key="index"
          :class="{ 'highlighted': item.special ,'nothighlighted' : !item.special}">
      {{ item.text }}
      <br>
    </span>
        </ul>
      </div>
    </div>
  </div>

</template>

<script setup>
import {ref, onMounted, onBeforeUnmount ,watch} from 'vue';
import buttonchangesize from './buttonchangesize.vue'
import { defineEmits } from 'vue';
const emit = defineEmits(['fullsize']);
const changesize =()=>{
  emit('fullsize');
}
const props=defineProps({
  cover:String,
  source:String,
  singer:String,
  name:String,
  lyrics:Array,
  sty:String,
})

const isPlaying = ref(false);
const durationtime = ref('0:00');
const currenttime = ref('0:00');
const currentduration = ref(0);
const maxlength = ref(100);

const lyricsshow = ref([{text: '', special: false}, {text: '', special: false}, {text: '', special: false}, {
  text: '',
  special: false
}, {text: '', special: false}, {text: '', special: false}, {text: '', special: false}, {
  text: '',
  special: false
}, {text: '', special: false}, {text: '', special: false}]);
const text = ref('未播放');
const nowline = ref(0);


const handleChange = () => {
  if (audioPlayer.value) {
    audioPlayer.value.currentTime = currentduration.value;
  }
};


// const handleFileChange = (event) => {
//   const file = event.target.files[0];
//   selectedFile.value = file;
//   audioSrc.value = URL.createObjectURL(file);
// };

const playAudio = () => {
  isPlaying.value = true;
  audioPlayer.value.play();
  const content = document.querySelector('.content');
  content.classList.add('rotate');
  content.classList.remove('stop');
};

const pauseAudio = () => {
  const content = document.querySelector('.content');
  isPlaying.value = false;
  audioPlayer.value.pause();
  content.classList.add('stop');
  content.classList.remove('rotate');
};

const togglePlay = () => {
  if (isPlaying.value) {
    pauseAudio();
  } else {
    playAudio();
  }
};

const restart = () => {
  if (audioPlayer.value) {
    audioPlayer.value.currentTime = 0; // 重置音频播放位置到开始
    audioPlayer.value.play(); // 播放音频
  }
};

const getCurrentTime = () => {
  const currentTime = audioPlayer.value.currentTime;
  const minute = Math.floor(currentTime / 60);
  const second = Math.floor(currentTime % 60);
  currenttime.value = `${minute}:${second < 10 ? '0' : ''}${second}`;
  currentduration.value = minute * 60 + second;
  displayLyrics(props.lyrics, currentduration.value);
};

const getDuration = () => {
  const duration = audioPlayer.value.duration;
  const minute = Math.floor(duration / 60);
  const second = Math.floor(duration % 60);
  durationtime.value = `${minute}:${second}`;
  maxlength.value = minute * 60 + second;
};

const audioPlayer = ref(null);

onMounted(() => {
  audioPlayer.value.addEventListener('timeupdate', getCurrentTime);
});

onBeforeUnmount(() => {
  audioPlayer.value.removeEventListener('timeupdate', getCurrentTime);
});

// function parseLRC(lrc) {
//   const lines = lrc.split('\n');
//   const lyrics = [];
//   const timeRegex = /\[(\d{2}):(\d{2})\.(\d{2})\](.*)/;

//   lines.forEach(line => {
//     const match = timeRegex.exec(line);
//     if (match) {
//       const minute = parseInt(match[1]);
//       const second = parseInt(match[2]);
//       const millisecond = parseInt(match[3]);
//       const timestamp = minute * 60 + second + millisecond / 1000;
//       const text = match[4].trim();
//       lyrics.push({timestamp, text});
//     }
//   });
//   return lyrics;
// }

function displayLyrics(lyrics, currentTime) {
  console.log(currentTime)
  for (let i = 0; i < lyrics.length; i++) {
    if (currentTime >= lyrics[i].timestamp && (!lyrics[i + 1] || currentTime < lyrics[i + 1].timestamp)) {
      text.value = lyrics[i].text;
      if (i <= 5) {
        let j = 0;
        for (j = 0; j < 10; ++j) {
          lyricsshow.value[j].text = lyrics[j].text;
          lyricsshow.value[j].special = false;
        }
        nowline.value = i;
        lyricsshow.value[nowline.value].special = true;
      } else if (i + 5 >= lyrics.length) {
        let j = 0;
        for (j = lyrics.length - 10; j < lyrics.length; ++j) {
          lyricsshow.value[j - lyrics.length + 10].text = lyrics[j].text;
          lyricsshow.value[j - lyrics.length + 10].special = false;
        }
        nowline.value = i - lyrics.length + 10;
        lyricsshow.value[nowline.value].special = true;
      } else {
        let j = 0;
        for (j = 0; j < 10; ++j) {
          lyricsshow.value[j].text = lyrics[j + i - 5].text;
          lyricsshow.value[j].special = false
        }
        nowline.value = 5;
        lyricsshow.value[nowline.value].special = true;
      }
      break;
    }
  }
}

</script>


<style scoped>
@import url('../css/Music_Play.css');

.outcontainer {
    display: grid;
    height:100%;
    grid-template-columns: 1fr 1fr;
}

.content {
  transform-origin: center center;
  animation: rotate 10s linear infinite;
}

.content.rotate {
  animation: rotate 10s linear infinite; /* 启动动画 */
}

.content.stop {
  animation-play-state: paused;
}

@keyframes rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.highlighted {
  display: block; /* 或 inline-block */
  width: 100%; /* 例如：指定一个宽度 */
  margin: 0 auto; /* 水平居中 */
  color: rgb(0, 0, 0, 0.5);
  font-weight: bolder;
  font-size: 250%;
  line-height: 2;
  text-align: center;
}

.nothighlighted {
  display: block; /* 或 inline-block */
  width: 100%; /* 例如：指定一个宽度 */
  margin: 0 auto; /* 水平居中 */
  color: rgb(0, 0, 0, 0.5);
  line-height: 2.5;
  font-size: 170%;
  text-align: center;
}

.box {
  border-radius: 10px;
  transition: width 0.5s, height 0.5s, background-color 0.5s;
}

.blur-enter-active,
.blur-leave-active {
  border-radius: 10px;
  transition: filter 0.5s; /* 定义过渡动画 */
}

.blur-enter,
.blur-leave-to {
  border-radius: 10px;
  filter: blur(5px); /* 初始和结束状态 */
}

.box:hover {
  border-radius: 10px;
  background-color: rgb(255, 255, 255, 0.2);
}
</style>
