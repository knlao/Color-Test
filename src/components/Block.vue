<template>
  <div
    class="box"
    :style="{ backgroundColor: color }"
    @click="handleClick"
  ></div>
</template>

<script setup>
const { color, isDiff } = defineProps(["color", "isDiff"]);
const emit = defineEmits(["correct"]);

const handleClick = () => {
  if (isDiff === "true") {
    alert("You are correct");
    emit("correct");
  }
};
</script>

<style scoped>
.box {
  width: 100px;
  height: 100px;
  border-radius: 10px;
  margin: 5px;
}
</style>