<template>
  <aside class="modern-sidebar">
    <div class="sidebar-container">
      <!-- Logo Section -->
      <div class="sidebar-logo">
        <div class="logo-icon">
          <svg width="32" height="32" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
            <rect width="32" height="32" rx="8" fill="url(#gradient1)"/>
            <path d="M16 8L22 12V20L16 24L10 20V12L16 8Z" fill="white" opacity="0.9"/>
            <defs>
              <linearGradient id="gradient1" x1="0" y1="0" x2="32" y2="32">
                <stop stop-color="#4F46E5"/>
                <stop offset="1" stop-color="#7C3AED"/>
              </linearGradient>
            </defs>
          </svg>
        </div>
        <div class="logo-text">
          <span class="logo-name">Valemis</span>
          <span class="logo-subtitle">ERP System</span>
        </div>
      </div>

    <!-- Navigation -->
    <nav class="sidebar-nav">
      <!-- MENU Section -->
      <div class="nav-section">
        <div class="section-label">MENU</div>
        
        <router-link to="/" class="nav-item" :class="{ active: route.path === '/' }">
          <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
            <path d="M10.707 2.293a1 1 0 00-1.414 0l-7 7a1 1 0 001.414 1.414L4 10.414V17a1 1 0 001 1h2a1 1 0 001-1v-2a1 1 0 011-1h2a1 1 0 011 1v2a1 1 0 001 1h2a1 1 0 001-1v-6.586l.293.293a1 1 0 001.414-1.414l-7-7z"/>
          </svg>
          <span>Dashboard</span>
        </router-link>

        <div class="nav-item" :class="{ active: isStakeholderActive }" @click="toggleSubmenu('stakeholder')">
          <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
            <path d="M9 6a3 3 0 11-6 0 3 3 0 016 0zM17 6a3 3 0 11-6 0 3 3 0 016 0zM12.93 17c.046-.327.07-.66.07-1a6.97 6.97 0 00-1.5-4.33A5 5 0 0119 16v1h-6.07zM6 11a5 5 0 015 5v1H1v-1a5 5 0 015-5z"/>
          </svg>
          <span>Stakeholder</span>
          <svg class="nav-arrow" :class="{ open: submenuOpen.stakeholder }" width="16" height="16" viewBox="0 0 16 16" fill="currentColor">
            <path d="M4.646 6.646a.5.5 0 01.708 0L8 9.293l2.646-2.647a.5.5 0 01.708.708l-3 3a.5.5 0 01-.708 0l-3-3a.5.5 0 010-.708z"/>
          </svg>
        </div>
        <div class="nav-submenu" v-show="submenuOpen.stakeholder">
          <router-link to="/stake-holder" class="submenu-item">Basic Management</router-link>
          <router-link to="/stakeholder-advanced" class="submenu-item">Advanced Analytics</router-link>
        </div>

        <router-link to="/pembebasan-lahan" class="nav-item" :class="{ active: route.path.startsWith('/pembebasan-lahan') }">
          <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M4 4a2 2 0 012-2h4.586A2 2 0 0112 2.586L15.414 6A2 2 0 0116 7.414V16a2 2 0 01-2 2H6a2 2 0 01-2-2V4z" clip-rule="evenodd"/>
          </svg>
          <span>Pembebasan Lahan</span>
        </router-link>

        <router-link to="/litigasi" class="nav-item" :class="{ active: route.path.startsWith('/litigasi') }">
          <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M8.257 3.099c.765-1.36 2.722-1.36 3.486 0l5.58 9.92c.75 1.334-.213 2.98-1.742 2.98H4.42c-1.53 0-2.493-1.646-1.743-2.98l5.58-9.92zM11 13a1 1 0 11-2 0 1 1 0 012 0zm-1-8a1 1 0 00-1 1v3a1 1 0 002 0V6a1 1 0 00-1-1z" clip-rule="evenodd"/>
          </svg>
          <span>Litigasi</span>
        </router-link>

        <router-link to="/larap" class="nav-item" :class="{ active: route.path === '/larap' }">
          <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
            <path d="M2 6a2 2 0 012-2h12a2 2 0 012 2v2a2 2 0 100 4v2a2 2 0 01-2 2H4a2 2 0 01-2-2v-2a2 2 0 100-4V6z"/>
          </svg>
          <span>LARAP</span>
        </router-link>
      </div>

      <!-- INVENTORY Section -->
      <div class="nav-section">
        <div class="section-label">INVENTORY & DATA</div>
        
        <router-link to="/aset-inventori" class="nav-item" :class="{ active: route.path.startsWith('/aset-inventori') }">
          <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
            <path d="M4 3a2 2 0 100 4h12a2 2 0 100-4H4z"/>
            <path fill-rule="evenodd" d="M3 8h14v7a2 2 0 01-2 2H5a2 2 0 01-2-2V8zm5 3a1 1 0 011-1h2a1 1 0 110 2H9a1 1 0 01-1-1z" clip-rule="evenodd"/>
          </svg>
          <span>Asset Inventory</span>
        </router-link>

        <router-link to="/land-inventory" class="nav-item" :class="{ active: route.path === '/land-inventory' }">
          <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm0 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm0 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z" clip-rule="evenodd"/>
          </svg>
          <span>Land Inventory</span>
        </router-link>

        <router-link to="/pendataan-geospatial" class="nav-item" :class="{ active: route.path === '/pendataan-geospatial' }">
          <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M5.05 4.05a7 7 0 119.9 9.9L10 18.9l-4.95-4.95a7 7 0 010-9.9zM10 11a2 2 0 100-4 2 2 0 000 4z" clip-rule="evenodd"/>
          </svg>
          <span>Geospatial Data</span>
        </router-link>

        <router-link to="/land-compliance" class="nav-item" :class="{ active: route.path === '/land-compliance' }">
          <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M6.267 3.455a3.066 3.066 0 001.745-.723 3.066 3.066 0 013.976 0 3.066 3.066 0 001.745.723 3.066 3.066 0 012.812 2.812c.051.643.304 1.254.723 1.745a3.066 3.066 0 010 3.976 3.066 3.066 0 00-.723 1.745 3.066 3.066 0 01-2.812 2.812 3.066 3.066 0 00-1.745.723 3.066 3.066 0 01-3.976 0 3.066 3.066 0 00-1.745-.723 3.066 3.066 0 01-2.812-2.812 3.066 3.066 0 00-.723-1.745 3.066 3.066 0 010-3.976 3.066 3.066 0 00.723-1.745 3.066 3.066 0 012.812-2.812zm7.44 5.252a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"/>
          </svg>
          <span>Land Compliance</span>
        </router-link>
      </div>

      <!-- TOOLS Section -->
      <div class="nav-section">
        <div class="section-label">TOOLS</div>
        
        <a href="#" class="nav-item">
          <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M11.49 3.17c-.38-1.56-2.6-1.56-2.98 0a1.532 1.532 0 01-2.286.948c-1.372-.836-2.942.734-2.106 2.106.54.886.061 2.042-.947 2.287-1.561.379-1.561 2.6 0 2.978a1.532 1.532 0 01.947 2.287c-.836 1.372.734 2.942 2.106 2.106a1.532 1.532 0 012.287.947c.379 1.561 2.6 1.561 2.978 0a1.533 1.533 0 012.287-.947c1.372.836 2.942-.734 2.106-2.106a1.533 1.533 0 01.947-2.287c1.561-.379 1.561-2.6 0-2.978a1.532 1.532 0 01-.947-2.287c.836-1.372-.734-2.942-2.106-2.106a1.532 1.532 0 01-2.287-.947zM10 13a3 3 0 100-6 3 3 0 000 6z" clip-rule="evenodd"/>
          </svg>
          <span>Settings</span>
        </a>

        <a href="#" class="nav-item">
          <svg class="nav-icon" width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-8-3a1 1 0 00-.867.5 1 1 0 11-1.731-1A3 3 0 0113 8a3.001 3.001 0 01-2 2.83V11a1 1 0 11-2 0v-1a1 1 0 011-1 1 1 0 100-2zm0 8a1 1 0 100-2 1 1 0 000 2z" clip-rule="evenodd"/>
          </svg>
          <span>Help</span>
        </a>
      </div>
    </nav>
    </div>
  </aside>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()

const submenuOpen = ref<Record<string, boolean>>({
  stakeholder: false
})

const isStakeholderActive = computed(() => {
  return route.path.startsWith('/stake-holder') || route.path.startsWith('/stakeholder-advanced')
})

const toggleSubmenu = (menu: string) => {
  submenuOpen.value[menu] = !submenuOpen.value[menu]
}
</script>

<style scoped>
.modern-sidebar {
  width: 260px;
  height: calc(100vh - 32px);
  position: fixed;
  left: 16px;
  top: 16px;
  z-index: 1000;
}

.sidebar-container {
  height: 100%;
  background: #F7F8FB;
  border-radius: 20px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.06);
  display: flex;
  flex-direction: column;
  overflow-y: auto;
  padding: 24px 16px;
}

/* Logo Section */
.sidebar-logo {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 0 8px 24px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.06);
  margin-bottom: 24px;
}

.logo-icon {
  flex-shrink: 0;
}

.logo-text {
  display: flex;
  flex-direction: column;
}

.logo-name {
  font-size: 18px;
  font-weight: 700;
  color: #111827;
  line-height: 1.2;
}

.logo-subtitle {
  font-size: 11px;
  color: #6B7280;
  font-weight: 500;
}

/* Navigation */
.sidebar-nav {
  flex: 1;
  overflow-y: auto;
}

.nav-section {
  margin-bottom: 24px;
}

.section-label {
  font-size: 11px;
  font-weight: 600;
  color: #9CA3AF;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  padding: 0 12px;
  margin-bottom: 8px;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 10px 12px;
  border-radius: 10px;
  color: #6B7280;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s ease;
  text-decoration: none;
  margin-bottom: 4px;
  position: relative;
}

.nav-item:hover {
  background: #F9FAFB;
  color: #374151;
}

.nav-item.active {
  background: linear-gradient(135deg, #4F46E5 0%, #6366F1 100%);
  color: #FFFFFF;
  box-shadow: 0 4px 12px rgba(79, 70, 229, 0.25);
}

.nav-icon {
  flex-shrink: 0;
  width: 20px;
  height: 20px;
}

.nav-arrow {
  margin-left: auto;
  transition: transform 0.2s ease;
}

.nav-arrow.open {
  transform: rotate(180deg);
}

.nav-submenu {
  margin-left: 32px;
  margin-top: 4px;
  margin-bottom: 8px;
}

.submenu-item {
  display: block;
  padding: 8px 12px;
  color: #6B7280;
  font-size: 13px;
  font-weight: 500;
  text-decoration: none;
  border-radius: 8px;
  transition: all 0.2s ease;
  margin-bottom: 2px;
}

.submenu-item:hover {
  background: #F9FAFB;
  color: #374151;
}

.submenu-item.router-link-active {
  color: #4F46E5;
  background: #EEF2FF;
}

/* Upgrade Card */
.upgrade-card {
  background: linear-gradient(135deg, #1F2937 0%, #111827 100%);
  border-radius: 16px;
  padding: 20px;
  margin-top: 16px;
  color: #FFFFFF;
}

.upgrade-icon {
  width: 48px;
  height: 48px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 16px;
}

.upgrade-title {
  font-size: 16px;
  font-weight: 700;
  margin-bottom: 4px;
}

.upgrade-subtitle {
  font-size: 12px;
  color: #D1D5DB;
  line-height: 1.4;
  margin-bottom: 16px;
}

.upgrade-button {
  width: 100%;
  padding: 10px 16px;
  background: #4F46E5;
  color: #FFFFFF;
  border: none;
  border-radius: 10px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s ease;
}

.upgrade-button:hover {
  background: #4338CA;
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(79, 70, 229, 0.4);
}

/* Scrollbar */
.modern-sidebar::-webkit-scrollbar {
  width: 6px;
}

.modern-sidebar::-webkit-scrollbar-track {
  background: transparent;
}

.modern-sidebar::-webkit-scrollbar-thumb {
  background: #E5E7EB;
  border-radius: 3px;
}

.modern-sidebar::-webkit-scrollbar-thumb:hover {
  background: #D1D5DB;
}
</style>
