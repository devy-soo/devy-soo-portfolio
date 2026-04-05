<script setup lang="ts">
import { computed, onMounted, onUnmounted, ref } from 'vue'
import HomePage from './pages/HomePage.vue'
import ContactPage from './pages/ContactPage.vue'

const baseUrl = import.meta.env.BASE_URL

const normalizePath = (pathname: string) => {
  const withoutBase = pathname.startsWith(baseUrl)
    ? pathname.slice(baseUrl.length - 1)
    : pathname

  return withoutBase || '/'
}

const path = ref(normalizePath(window.location.pathname))

const syncPath = () => {
  path.value = normalizePath(window.location.pathname)
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
        <a :href="baseUrl">Home</a>
        <a :href="`${baseUrl}contact`">Contact</a>
      </nav>
    </header>

    <main>
      <component :is="CurrentPage" />
    </main>
  </div>
</template>
