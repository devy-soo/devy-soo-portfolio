<script setup lang="ts">
import { computed, onMounted, onUnmounted, ref } from 'vue'
import HomePage from './pages/HomePage.vue'
import ContactPage from './pages/ContactPage.vue'

const path = ref(window.location.pathname)

const syncPath = () => {
  path.value = window.location.pathname
}

onMounted(() => {
  window.addEventListener('popstate', syncPath)
})

onUnmounted(() => {
  window.removeEventListener('popstate', syncPath)
})

const CurrentPage = computed(() => {
  if (path.value === '/contact') {
    return ContactPage
  }

  return HomePage
})
</script>

<template>
  <div class="site-shell">
    <header class="site-header">
      <nav class="site-nav">
        <a href="/">Home</a>
        <a href="/contact">Contact</a>
      </nav>
    </header>

    <main>
      <component :is="CurrentPage" />
    </main>
  </div>
</template>
