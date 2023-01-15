<script setup>
import { ref, onMounted, onBeforeMount } from 'vue';

defineProps({});

defineExpose({
  resize: onResize,
});

const cards = 6;

const container = ref(null);

const features = ref(null);

const content = ref(null);

const moreButton = ref(null);

const moreButtonVisible = ref(false);

const morePopupDisplayed = ref(false);

const morePopup = ref(null);

function onResize() {
  resetMore();
  handleMore();
}

function resetMore() {
  const children = [...morePopup.value.children];
  // iterate over all child nodes
  for (let i = 0; i < children.length; i++) {
    let element = children[i];
    content.value.insertBefore(element, moreButton.value);
  }
  moreButtonVisible.value = false;
}

function handleMore() {
  let containerWidth = container.value.offsetWidth;
  let width = features.value.offsetWidth; // more button is assumed as "displayed"
  let buttonV = false;
  for (let i = 0; i < cards; i++) {
    let card = document.getElementById('card' + (i - 1));
    width += 70 + 4; // 4 for margin
    if (width > containerWidth) {
      buttonV = true; // display the more button
      morePopup.value.appendChild(card);
    }
  }
  moreButtonVisible.value = buttonV;
  if (buttonV) {
    let card = document.getElementById('card' + (cards - 1));
    morePopup.value.appendChild(card);
  }
}

onBeforeMount(() => {});

onMounted(() => {
  handleMore();
});

function onMoreClick() {
  morePopupDisplayed.value = !morePopupDisplayed.value;
}
</script>

<template>
  <div class="container" ref="container">
    <div class="container-cnt" ref="content">
      <div class="card" v-for="n in cards" :id="`card${n - 1}`">
        {{ n }}
      </div>
      <button
        class="moreButton"
        ref="moreButton"
        v-show="moreButtonVisible"
        @click="onMoreClick"
      >
        More
      </button>
    </div>
    <div class="features" ref="features">Features</div>
    <div class="morePopup" ref="morePopup" v-show="morePopupDisplayed"></div>
  </div>
</template>

<style scoped>
.container {
  display: grid;
  grid-template-columns: auto 200px;
  background-color: lightblue;
  max-height: 30px;
}

.container-cnt {
  display: flex;
  background-color: lightcoral;
}

.features {
  display: inline-block;
  width: auto;
  background-color: yellow;
  height: 20px;
  margin: 2px;
  color: black;
  line-height: 21px;
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
  top: 70px;
  right: 8px;
  display: flex;
  flex-direction: column;
}
</style>
