<script setup lang="ts">
import { ref } from "vue";
import AmbientContainer from "./components/AmbientContainer.vue";
const rootClass = "page";

const ambientStatus = ref(false);
</script>

<template>
  <div :class="rootClass">
    <button class="button" @click="ambientStatus = !ambientStatus">
      Turn Ambient Mode {{ !ambientStatus ? "On" : "Off" }}
    </button>
    <AmbientContainer :ambientOn="ambientStatus" />
    <AmbientContainer :ambientOn="ambientStatus" />
    <AmbientContainer :ambientOn="ambientStatus" />
    <AmbientContainer :ambientOn="ambientStatus" />
  </div>
</template>

<style scoped></style>
