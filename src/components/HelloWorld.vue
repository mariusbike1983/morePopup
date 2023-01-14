<script setup>
import { ref, onMounted, onBeforeMount } from 'vue';

defineProps({});

defineExpose({
  resize: onResize,
});

const cards = 10;
const vc = ref([]);

const container = ref(null);

const moreButtonVisible = ref(false);

const morePopupDisplayed = ref(false);

const morePopup = ref(null);

function onResize() {
  console.log('resizing');
}

onBeforeMount(() => {
  for (let i = 0; i < cards; i++) {
    vc.value.push(true);
  }
});

onMounted(() => {
  let containerWidth = container.value.offsetWidth;
  let width = 70; // more button is assumed as "displayed"
  let buttonV = false;
  let moreIndex = -1;
  for (let i = 0; i < cards; i++) {
    width += 70;
    if (width >= containerWidth) {
      buttonV = true; // display the more button
      console.log('must hide the button ' + i);
      let card = document.getElementById('card' + i);
      morePopup.value.appendChild(card);
      // vc.value[i] = false; // hide
      // if (moreIndex < 0) {
      //   moreIndex = i;
      // }
    }
  }
  moreButtonVisible.value = buttonV;
});

function onMoreClick() {
  morePopupDisplayed.value = !morePopupDisplayed.value;
}
</script>

<template>
  <div class="container" ref="container">
    <div
      class="card"
      v-for="n in cards"
      v-show="vc[n - 1]"
      :id="`card${n - 1}`"
    >
      {{ n - 1 }}
    </div>
    <button class="moreButton" v-show="moreButtonVisible" @click="onMoreClick">
      More
    </button>
    <div class="morePopup" ref="morePopup" v-show="morePopupDisplayed"></div>
  </div>
</template>

<style scoped>
.container {
  background-color: lightblue;
  max-height: 30px;
  display: flex;
}

.card {
  display: inline-block;
  width: 70px;
  min-width: 70px;
  height: 20px;
  margin: 2px;
  background-color: blue;
}

.moreButton {
  display: inline-block;
  width: 70px;
  min-width: 70px;
  height: 20px;
  margin: 2px;
  background-color: red;
  color: white;
}

.morePopup {
  position: absolute;
  width: 75px;
  height: auto;
  background-color: red;
  top: 40px;
  right: 8px;
  display: flex;
  flex-direction: column;
}
</style>
