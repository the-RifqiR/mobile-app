<script setup>
// script section
import { RouterView } from 'vue-router';
</script>

<template>
  <!-- template section  -->
  <RouterView v-slot="{ Component }">
    <transition name="page" mode="out-in">
      <component :is="Component" />
    </transition>
  </RouterView>
</template>

<style>
/* Global styles */
body {
  margin: 0;
  padding: 0;
  min-height: 100vh;
  background: linear-gradient(135deg, #1a237e 0%, #0d47a1 50%, #000000 100%);
  font-family: sans-serif;
}

/* Page transition effects */
.page-enter-active,
.page-leave-active {
  transition: all 0.5s;
}

.page-enter-from,
.page-leave-to {
  opacity: 0;
  transform: scale(0.95);
  filter: blur(10px);
}

.page-enter-active {
  animation: pageGlitch 0.5s;
}

@keyframes pageGlitch {
  0% {
    transform: translate(0);
    filter: hue-rotate(0deg) blur(0);
  }
  20% {
    transform: translate(-5px, 5px);
    filter: hue-rotate(90deg) blur(2px);
  }
  40% {
    transform: translate(-5px, -5px);
    filter: hue-rotate(180deg) blur(4px);
  }
  60% {
    transform: translate(5px, 5px);
    filter: hue-rotate(270deg) blur(2px);
  }
  80% {
    transform: translate(5px, -5px);
    filter: hue-rotate(360deg) blur(1px);
  }
  100% {
    transform: translate(0);
    filter: hue-rotate(0deg) blur(0);
  }
}

/* Glitch text effect */
.glitch-text {
  position: relative;
  display: inline-block;
}

.glitch-text::before,
.glitch-text::after {
  content: attr(data-text);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0.8;
}

.glitch-text::before {
  color: #ff00ff;
  z-index: -1;
  animation: glitch-effect 3s infinite;
}

.glitch-text::after {
  color: #00ffff;
  z-index: -2;
  animation: glitch-effect 2s infinite reverse;
}

@keyframes glitch-effect {
  0% {
    transform: translate(0);
  }
  20% {
    transform: translate(-3px, 3px);
  }
  40% {
    transform: translate(-3px, -3px);
  }
  60% {
    transform: translate(3px, 3px);
  }
  80% {
    transform: translate(3px, -3px);
  }
  100% {
    transform: translate(0);
  }
}
</style>