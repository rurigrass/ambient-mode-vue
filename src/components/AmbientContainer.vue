<template>
  <div class="container">
    <canvas class="canvas" ref="canvasRef"></canvas>
    <video
      class="video"
      ref="videoRef"
      controls
      autoPlay
      muted
      loop
      src="../assets/AmbientModeTest.mp4"
    ></video>
  </div>
</template>

<script setup lang="ts">
import { ref, defineProps, onUpdated } from "vue";
const props = defineProps<{ ambientOn: boolean }>();

const videoRef = ref<HTMLVideoElement>();
const canvasRef = ref<HTMLCanvasElement>();

onUpdated(() => {
  const canvas = canvasRef.value;
  const video = videoRef.value;
  if (!video || !canvas) return;
  const ctx = canvas.getContext("2d");
  if (!ctx) return;
  drawAmbient(ctx, canvas, video, props.ambientOn);
  !props.ambientOn && ctx.clearRect(0, 0, canvas.width, canvas.height);
});

const drawAmbient = (
  ctx: CanvasRenderingContext2D,
  canvas: HTMLCanvasElement,
  video: HTMLVideoElement,
  ambient: boolean
) => {
  ctx.drawImage(video, 0, 0, 1, 1, 0, 0, canvas.width, canvas.height);
  video.ontimeupdate = () => {
    ambient
      ? ctx.drawImage(video, 0, 0, 1, 1, 0, 0, canvas.width, canvas.height)
      : ctx.clearRect(0, 0, canvas.width, canvas.height);
  };
};
</script>

<style scoped></style>
