<template>
<input v-model="text"/>
<p>{{ text }}</p>
<!-- <audio src="./难得有情人.mp3" controls></audio> -->
<button @click="change" class="btn btn-primary">点击改变</button>
</template>

<script setup>
import { ref } from 'vue';
const text = ref('hello');
const change = () => {
  text.value = 'world';
}
</script>

