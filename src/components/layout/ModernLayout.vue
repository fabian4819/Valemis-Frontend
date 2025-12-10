<template>
  <div class="modern-layout">
    <ModernSidebar />
    
    <div class="main-content">
      <ModernHeader 
        :page-title="pageTitle" 
        :page-subtitle="pageSubtitle" 
      />
      
      <div class="content-wrapper">
        <slot />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useRoute } from 'vue-router'
import ModernSidebar from './ModernSidebar.vue'
import ModernHeader from './ModernHeader.vue'

const route = useRoute()

const pageTitles: Record<string, { title: string; subtitle: string }> = {
  '/': {
    title: 'Dashboard',
    subtitle: 'Welcome back! Here\'s what\'s happening with your projects today.'
  },
  '/stakeholder-advanced': {
    title: 'Stakeholder Management',
    subtitle: 'Advanced analytics and sentiment analysis for stakeholder relationships'
  },
  '/stake-holder': {
    title: 'Stakeholder Management',
    subtitle: 'Manage and monitor stakeholder information'
  },
  '/pembebasan-lahan': {
    title: 'Pembebasan Lahan',
    subtitle: 'Land acquisition and compensation management'
  },
  '/litigasi': {
    title: 'Litigasi & Claim',
    subtitle: 'Manage litigation cases and land claims'
  },
  '/larap': {
    title: 'LARAP Management',
    subtitle: 'Land Acquisition and Resettlement Action Plan'
  },
  '/aset-inventori': {
    title: 'Asset Inventory',
    subtitle: 'Track and manage all asset inventories'
  },
  '/land-inventory': {
    title: 'Land Inventory',
    subtitle: 'Comprehensive land data and spatial information'
  },
  '/pendataan-geospatial': {
    title: 'Geospatial Data',
    subtitle: 'Interactive maps and geographic information system'
  },
  '/land-compliance': {
    title: 'Land Compliance',
    subtitle: 'Monitor land compliance and regulatory requirements'
  }
}

const pageTitle = computed(() => {
  return pageTitles[route.path]?.title || 'Page'
})

const pageSubtitle = computed(() => {
  return pageTitles[route.path]?.subtitle || 'Manage your data'
})
</script>

<style scoped>
.modern-layout {
  display: flex;
  min-height: 100vh;
  background: #EDEDF9;
}

.main-content {
  flex: 1;
  margin-left: 292px;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.content-wrapper {
  flex: 1;
  padding: 32px;
  padding-top: 16px;
  overflow-x: hidden;
}

@media (max-width: 1024px) {
  .main-content {
    margin-left: 0;
  }
}
</style>
