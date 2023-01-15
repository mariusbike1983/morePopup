<script setup>
import HelloWorld from './components/HelloWorld.vue';
import { ref } from 'vue';

const toolbar = ref('HelloWorld');

function doResize() {
  toolbar.value?.resize();
}
</script>

<template>
  <button class="resize" @click="doResize">Resize</button>

  <HelloWorld ref="toolbar" />
</template>

<style scoped>
.resize {
}
</style>
