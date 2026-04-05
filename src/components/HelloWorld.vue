<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'

const offsetX = ref(0)

const updateOffset = () => {
  const maxShift = window.innerWidth * 0.35
  const maxScroll = window.innerHeight * 1.2
  const progress = Math.min(window.scrollY / maxScroll, 1)
  offsetX.value = maxShift * progress
}

onMounted(() => {
  updateOffset()
  window.addEventListener('scroll', updateOffset, { passive: true })
  window.addEventListener('resize', updateOffset)
})

onUnmounted(() => {
  window.removeEventListener('scroll', updateOffset)
  window.removeEventListener('resize', updateOffset)
})
</script>

<template>
  <section class="hero-scroll">
    <div class="hero-scroll__sticky" :style="{ '--offset-x': `${offsetX}px` }">
      <p class="hero-scroll__line hero-scroll__line--left">
        CREATIVE CONNECTIONS · CREATIVE CONNECTIONS · CREATIVE CONNECTIONS
      </p>
      <p class="hero-scroll__line hero-scroll__line--right">
        CREATIVE CONNECTIONS · CREATIVE CONNECTIONS · CREATIVE CONNECTIONS
      </p>
    </div>
  </section>
</template>
