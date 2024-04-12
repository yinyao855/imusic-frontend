<template>
<input v-model="text"/>
<p>{{ text }}</p>
<audio src="./难得有情人.mp3" controls></audio>
</template>

<script setup>
import { ref } from 'vue';
const text = ref('hello');
</script>

