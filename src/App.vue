<template>
  <ModernLayout>
    <router-view />
  </ModernLayout>
</template>

<script setup lang="ts">
import ModernLayout from './components/layout/ModernLayout.vue'
</script>

<style>
/* Import Google Fonts - Inter for modern look */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #F9FAFB;
  color: #111827;
}

#app {
  min-height: 100vh;
}
</style>
