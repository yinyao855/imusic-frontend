<template>
  <div class="flex justify-center">
    <img src="../assets/音乐桃.svg"  alt="音乐" class="w-48 h-48">
    <p class="text-4xl font-bold my-auto">Imusic Player</p>
  </div>

  <div class="overflow-x-auto w-3/5 mx-auto">
    <table class="table">
      <!-- head -->
      <thead>
      <tr>
        <th></th>
        <th>歌名</th>
        <th>作者</th>
        <th>播放</th>
      </tr>
      </thead>
      <tbody>
      <!-- rows -->
      <tr v-for="(row, index) in musicList" class="hover">
        <th>{{ index+1 }}</th>
        <td>{{ row.name }}</td>
        <td>{{ row.singer }}</td>
        <td>
          <button class="btn btn-info btn-outline btn-sm" @click="playMusic(index)">Play</button>
        </td>
      </tr>
      </tbody>
    </table>
  </div>

</template>

<script setup>
const emit = defineEmits([
    "playMusic",
])

const props = defineProps({
  musicList: Object,
})

function playMusic(index) {
    emit("playMusic",index);
}
</script>

