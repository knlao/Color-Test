<template>
  <h1>Color Test</h1>
  <h2>Which one is different?</h2>
  <div class="board">
    <div class="row" v-for="n in boardWidth" :key="n">
      <span v-for="m in boardWidth" :key="m">
        <span v-if="(n - 1) * boardWidth + m === randomIdx"
          ><Block :color="diffColor" isDiff="true" @correct="newColor"></Block
        ></span>
        <span v-else><Block :color="currentColor" isDiff="false"></Block></span>
      </span>
    </div>
  </div>
  <button @click="newColor">generate new color</button>

  <br />
  <h3 @click="isDebugging = !isDebugging">Debug use</h3>
  <div v-if="isDebugging">
    <p>Item: {{ randomIdx }}</p>
    <p>Current Color: {{ currentColor }}</p>
    <p>Different Color: {{ diffColor }}</p>
  </div>
</template>

<script setup>
import { ref } from "vue";
import Block from "./components/Block.vue";

const boardWidth = ref(4);
const currentColor = ref("#EEEEEE");
const diffColor = ref("#EDEDED");
const diffRate = ref(25);
const randomIdx = ref(
  Math.floor(Math.random() * (boardWidth.value * boardWidth.value) + 1)
);
const isDebugging = ref(false);

const newColor = () => {
  let g =
    Math.floor(Math.random() * (256 - diffRate.value * 2)) + diffRate.value;
  let r =
    Math.floor(Math.random() * (256 - diffRate.value * 2)) + diffRate.value;
  let b =
    Math.floor(Math.random() * (256 - diffRate.value * 2)) + diffRate.value;
  currentColor.value = "#" + r.toString(16) + g.toString(16) + b.toString(16);
  diffColor.value =
    "#" +
    Math.floor(r + Math.floor(Math.random() * diffRate.value)).toString(16) +
    Math.floor(g + Math.floor(Math.random() * diffRate.value)).toString(16) +
    Math.floor(b + Math.floor(Math.random() * diffRate.value)).toString(16);
  randomIdx.value = Math.floor(
    Math.random() * (boardWidth.value * boardWidth.value) + 1
  );
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.row {
  display: flex;
  justify-content: center;
}
</style>
