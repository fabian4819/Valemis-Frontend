<template>
  <aside class="app-sidebar bg-body-secondary shadow" data-bs-theme="dark">
    <div class="sidebar-brand">
      <router-link to="/" class="brand-link">
        <span class="brand-text fw-light">LM APP</span>
      </router-link>
    </div>
    
    <div class="sidebar-wrapper">
      <nav class="mt-2">
        <ul
          class="nav sidebar-menu flex-column"
          data-lte-toggle="treeview"
          role="navigation"
          aria-label="Main navigation"
          data-accordion="false"
          id="navigation"
        >
          <!-- Dashboard -->
          <li class="nav-item" :class="{ active: route.path === '/' }">
            <router-link to="/" class="nav-link">
              <i class="nav-icon bi bi-speedometer"></i>
              <p>Dashboard</p>
            </router-link>
          </li>

          <!-- LARAP Module -->
          <li class="nav-item" :class="{ active: route.path.startsWith('/larap') }">
            <router-link to="/larap" class="nav-link">
              <i class="nav-icon bi bi-clipboard-data"></i>
              <p>LARAP</p>
            </router-link>
          </li>

          <!-- Pembebasan Lahan Module -->
          <li class="nav-item" :class="{ active: route.path.startsWith('/pembebasan-lahan') }">
            <router-link to="/pembebasan-lahan" class="nav-link">
              <i class="nav-icon bi bi-map"></i>
              <p>Pembebasan Lahan</p>
            </router-link>
          </li>

          <!-- Pendataan Geospatial Lahan Bebas -->
          <li class="nav-item" :class="{ active: route.path.startsWith('/pendataan-geospatial') }">
            <router-link to="/pendataan-geospatial" class="nav-link">
              <i class="nav-icon bi bi-geo-alt-fill"></i>
              <p>Geospatial Lahan Bebas</p>
            </router-link>
          </li>

          <!-- Land Compliance Module -->
          <li class="nav-item" :class="{ active: route.path.startsWith('/land-compliance') }">
            <router-link to="/land-compliance" class="nav-link">
              <i class="nav-icon bi bi-shield-check"></i>
              <p>Land Compliance</p>
            </router-link>
          </li>
          
          <!-- Litigasi/Claim Lahan Module -->
          <li class="nav-item" :class="{ active: route.path.startsWith('/litigasi') }">
            <router-link to="/litigasi" class="nav-link">
              <i class="nav-icon bi bi-exclamation-triangle"></i>
              <p>Litigasi/Claim Lahan</p>
            </router-link>
          </li>

          <!-- Stakeholder Management Module -->
          <li class="nav-item" :class="{ active: route.path.startsWith('/stake-holder') || route.path.startsWith('/stakeholder-advanced') }">
            <a href="#" class="nav-link">
              <i class="nav-icon bi bi-people"></i>
              <p>
                Stakeholder Management
                <i class="right fas fa-angle-left"></i>
              </p>
            </a>
            <ul class="nav nav-treeview">
              <li class="nav-item">
                <router-link to="/stake-holder" class="nav-link" :class="{ active: route.path === '/stake-holder' }">
                  <i class="far fa-circle nav-icon"></i>
                  <p>Basic Management</p>
                </router-link>
              </li>
              <li class="nav-item">
                <router-link to="/stakeholder-advanced" class="nav-link" :class="{ active: route.path === '/stakeholder-advanced' }">
                  <i class="far fa-circle nav-icon"></i>
                  <p>Advanced Analytics</p>
                </router-link>
              </li>
            </ul>
          </li>

          <li class="nav-header">INVENTORY & DATA</li>

          <!-- Asset Inventory Module -->
          <li class="nav-item" :class="{ active: route.path.startsWith('/aset-inventori') }">
            <router-link to="/aset-inventori" class="nav-link">
              <i class="nav-icon bi bi-archive"></i>
              <p>Asset Inventory</p>
            </router-link>
          </li>

          <!-- Land Inventory Module -->
          <li class="nav-item" :class="{ active: route.path.startsWith('/land-inventory') }">
            <router-link to="/land-inventory" class="nav-link">
              <i class="nav-icon bi bi-layers"></i>
              <p>Land Inventory</p>
            </router-link>
          </li>
        </ul>
      </nav>
    </div>
  </aside>
</template>

<script setup lang="ts">
import { useRoute } from 'vue-router'

const route = useRoute()
</script>

<style scoped>
</style>
