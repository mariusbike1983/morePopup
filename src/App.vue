<script setup>
import Toolbar from './components/Toolbar.vue';
import { ref } from 'vue';

const toolbar = ref('Toolbar');

function doResize() {
  toolbar.value?.resize();
}
</script>

<template>
  <button class="resize" @click="doResize">Resize</button>

  <Toolbar ref="toolbar" />
</template>

<style scoped>
.resize {
}
</style>
