<template>
  <header class="modern-header">
    <div class="header-left">
      <h1 class="page-title">{{ pageTitle }}</h1>
      <p class="page-subtitle">{{ pageSubtitle }}</p>
    </div>

    <div class="header-right">
      <!-- Search -->
      <button class="header-icon-button" @click="toggleSearch">
        <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <circle cx="11" cy="11" r="8"></circle>
          <path d="m21 21-4.35-4.35"></path>
        </svg>
      </button>

      <!-- Notifications -->
      <button class="header-icon-button notification-button" @click="toggleNotifications">
        <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"></path>
          <path d="M13.73 21a2 2 0 0 1-3.46 0"></path>
        </svg>
        <span v-if="notificationCount > 0" class="notification-dot"></span>
      </button>

      <!-- Profile -->
      <div class="profile-section" @click="toggleProfile">
        <img 
          :src="userAvatar" 
          alt="User Avatar" 
          class="profile-avatar"
        >
        <div class="profile-info">
          <div class="profile-name">{{ userName }}</div>
          <div class="profile-role">{{ userRole }}</div>
        </div>
      </div>
    </div>

    <!-- Dropdowns Container -->
    <div class="dropdowns-container">
      <!-- Search Dropdown -->
      <transition name="fade">
        <div v-if="showSearch" class="dropdown search-dropdown">
          <div class="search-input-wrapper">
            <input 
              type="text" 
              class="search-input" 
              placeholder="Search anything..." 
              v-model="searchQuery"
              @keyup.enter="performSearch"
              autofocus
            >
          </div>
        </div>
      </transition>

      <!-- Notifications Dropdown -->
      <transition name="fade">
        <div v-if="showNotifications" class="dropdown notifications-dropdown">
          <div class="dropdown-header">
            <h3>Notifications</h3>
            <button class="mark-all-read">Mark all as read</button>
          </div>
          <div class="dropdown-content">
            <div v-for="notif in notifications" :key="notif.id" class="notification-item" :class="{ unread: !notif.read }">
              <div class="notification-icon" :class="notif.type">
                <svg v-if="notif.type === 'success'" width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.857-9.809a.75.75 0 00-1.214-.882l-3.483 4.79-1.88-1.88a.75.75 0 10-1.06 1.061l2.5 2.5a.75.75 0 001.137-.089l4-5.5z" clip-rule="evenodd" />
                </svg>
                <svg v-else-if="notif.type === 'warning'" width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M8.485 2.495c.673-1.167 2.357-1.167 3.03 0l6.28 10.875c.673 1.167-.17 2.625-1.516 2.625H3.72c-1.347 0-2.189-1.458-1.515-2.625L8.485 2.495zM10 5a.75.75 0 01.75.75v3.5a.75.75 0 01-1.5 0v-3.5A.75.75 0 0110 5zm0 9a1 1 0 100-2 1 1 0 000 2z" clip-rule="evenodd" />
                </svg>
                <svg v-else width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a.75.75 0 000 1.5h.253a.25.25 0 01.244.304l-.459 2.066A1.75 1.75 0 0010.747 15H11a.75.75 0 000-1.5h-.253a.25.25 0 01-.244-.304l.459-2.066A1.75 1.75 0 009.253 9H9z" clip-rule="evenodd" />
                </svg>
              </div>
              <div class="notification-content">
                <div class="notification-header">
                  <div class="notification-title">{{ notif.title }}</div>
                  <div class="notification-time">{{ notif.time }}</div>
                </div>
                <p class="notification-message">{{ notif.message }}</p>
              </div>
            </div>
          </div>
        </div>
      </transition>

      <!-- Profile Dropdown -->
      <transition name="fade">
        <div v-if="showProfile" class="dropdown profile-dropdown">
          <div class="profile-info">
            <div class="profile-avatar">
              <img :src="userAvatar" alt="Avatar">
            </div>
            <div class="profile-details">
              <h4>{{ userName }}</h4>
              <p>{{ userEmail }}</p>
            </div>
          </div>
          <div class="profile-menu">
            <a href="#" class="profile-menu-item">
              <svg width="16" height="16" viewBox="0 0 20 20" fill="currentColor" style="display: inline-block; margin-right: 8px;">
                <path d="M10 8a3 3 0 100-6 3 3 0 000 6zM3.465 14.493a1.23 1.23 0 00.41 1.412A9.957 9.957 0 0010 18c2.31 0 4.438-.784 6.131-2.1.43-.333.604-.903.408-1.41a7.002 7.002 0 00-13.074.003z" />
              </svg>
              My Profile
            </a>
            <a href="#" class="profile-menu-item">
              <svg width="16" height="16" viewBox="0 0 20 20" fill="currentColor" style="display: inline-block; margin-right: 8px;">
                <path fill-rule="evenodd" d="M7.84 1.804A1 1 0 018.82 1h2.36a1 1 0 01.98.804l.331 1.652a6.993 6.993 0 011.929 1.115l1.598-.54a1 1 0 011.186.447l1.18 2.044a1 1 0 01-.205 1.251l-1.267 1.113a7.047 7.047 0 010 2.228l1.267 1.113a1 1 0 01.206 1.25l-1.18 2.045a1 1 0 01-1.187.447l-1.598-.54a6.993 6.993 0 01-1.929 1.115l-.33 1.652a1 1 0 01-.98.804H8.82a1 1 0 01-.98-.804l-.331-1.652a6.993 6.993 0 01-1.929-1.115l-1.598.54a1 1 0 01-1.186-.447l-1.18-2.044a1 1 0 01.205-1.251l1.267-1.114a7.05 7.05 0 010-2.227L1.821 7.773a1 1 0 01-.206-1.25l1.18-2.045a1 1 0 011.187-.447l1.598.54A6.993 6.993 0 017.51 3.456l.33-1.652zM10 13a3 3 0 100-6 3 3 0 000 6z" clip-rule="evenodd" />
              </svg>
              Settings
            </a>
            <a href="#" class="profile-menu-item danger">
              <svg width="16" height="16" viewBox="0 0 20 20" fill="currentColor" style="display: inline-block; margin-right: 8px;">
                <path fill-rule="evenodd" d="M3 4.25A2.25 2.25 0 015.25 2h5.5A2.25 2.25 0 0113 4.25v2a.75.75 0 01-1.5 0v-2a.75.75 0 00-.75-.75h-5.5a.75.75 0 00-.75.75v11.5c0 .414.336.75.75.75h5.5a.75.75 0 00.75-.75v-2a.75.75 0 011.5 0v2A2.25 2.25 0 0110.75 18h-5.5A2.25 2.25 0 013 15.75V4.25z" clip-rule="evenodd" />
                <path fill-rule="evenodd" d="M19 10a.75.75 0 00-.75-.75H8.704l1.048-.943a.75.75 0 10-1.004-1.114l-2.5 2.25a.75.75 0 000 1.114l2.5 2.25a.75.75 0 101.004-1.114l-1.048-.943h9.546A.75.75 0 0019 10z" clip-rule="evenodd" />
              </svg>
              Logout
            </a>
          </div>
        </div>
      </transition>
    </div>
  </header>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface Props {
  pageTitle?: string
  pageSubtitle?: string
}

const props = withDefaults(defineProps<Props>(), {
  pageTitle: 'Dashboard',
  pageSubtitle: 'Welcome back! Here\'s what\'s happening with your projects today.'
})

const notificationCount = ref(3)
const userName = ref('Ferna Alexandra')
const userRole = ref('Admin Store')
const userEmail = ref('ferra@valemis.com')
const userAvatar = ref('https://ui-avatars.com/api/?name=Ferna+Alexandra&background=4F46E5&color=fff')

const showSearch = ref(false)
const showNotifications = ref(false)
const showProfile = ref(false)
const searchQuery = ref('')

const notifications = ref([
  {
    id: 1,
    type: 'success',
    title: 'Stakeholder Updated',
    message: 'Ahmad Sulaiman profile has been updated successfully',
    time: '2 minutes ago',
    read: false
  },
  {
    id: 2,
    type: 'warning',
    title: 'Pending Approval',
    message: 'New land acquisition requires your approval',
    time: '1 hour ago',
    read: false
  },
  {
    id: 3,
    type: 'info',
    title: 'System Update',
    message: 'System will be updated tonight at 02:00 AM',
    time: '3 hours ago',
    read: true
  }
])

const toggleSearch = () => {
  showSearch.value = !showSearch.value
  showNotifications.value = false
  showProfile.value = false
}

const toggleNotifications = () => {
  showNotifications.value = !showNotifications.value
  showSearch.value = false
  showProfile.value = false
}

const toggleProfile = () => {
  showProfile.value = !showProfile.value
  showSearch.value = false
  showNotifications.value = false
}

const performSearch = () => {
  console.log('Searching for:', searchQuery.value)
}
</script>

<style scoped>
.modern-header {
  background: #EDEDF9;
  padding: 24px 32px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: none;
  position: sticky;
  top: 0;
  z-index: 100;
  min-height: 88px;
}

.header-left {
  flex: 1;
}

.page-title {
  font-size: 28px;
  font-weight: 700;
  color: #111827;
  margin: 0 0 4px 0;
  line-height: 1.2;
}

.page-subtitle {
  font-size: 14px;
  color: #6B7280;
  margin: 0;
}

.header-right {
  display: flex;
  align-items: center;
  gap: 12px;
  position: relative;
}

.header-icon-button {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  border: none;
  background: #FFFFFF;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  color: #6B7280;
  transition: all 0.2s ease;
  position: relative;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
}

.header-icon-button:hover {
  background: #F9FAFB;
  color: #4F46E5;
  transform: translateY(-1px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.12);
}

.notification-button {
  position: relative;
}

.notification-dot {
  position: absolute;
  top: 10px;
  right: 10px;
  width: 8px;
  height: 8px;
  background: #EF4444;
  border-radius: 50%;
  border: 2px solid #FFFFFF;
}

.profile-section {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 4px;
  padding-right: 16px;
  border-radius: 50px;
  background: #FFFFFF;
  transition: all 0.2s ease;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
}

.profile-section:hover {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.12);
}

.profile-avatar {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid #FFFFFF;
}

.profile-info {
  display: flex;
  flex-direction: column;
}

.profile-name {
  font-size: 14px;
  font-weight: 600;
  color: #111827;
  line-height: 1.2;
}

.profile-role {
  font-size: 12px;
  color: #6B7280;
}

/* Dropdowns Container */
.dropdowns-container {
  position: relative;
}

/* Dropdown Styles */
.dropdown {
  position: absolute;
  top: 40px;
  right: 0;
  background: white;
  border-radius: 16px;
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
  z-index: 1000;
  min-width: 320px;
  overflow: hidden;
  animation: slideDown 0.2s ease-out;
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.dropdown-header {
  padding: 20px;
  border-bottom: 1px solid #F3F4F6;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.dropdown-header h3 {
  font-size: 18px;
  font-weight: 700;
  color: #111827;
  margin: 0;
}

.mark-all-read {
  font-size: 13px;
  color: #6B7280;
  background: #F3F4F6;
  border: none;
  padding: 6px 12px;
  border-radius: 6px;
  cursor: pointer;
  transition: all 0.2s;
}

.mark-all-read:hover {
  background: #E5E7EB;
  color: #4F46E5;
}

.dropdown-content {
  max-height: 400px;
  overflow-y: auto;
}

/* Search Dropdown */
.search-dropdown {
  min-width: 400px;
}

.search-input-wrapper {
  padding: 20px;
}

.search-input {
  width: 100%;
  padding: 12px 16px;
  border: 2px solid #E5E7EB;
  border-radius: 10px;
  font-size: 14px;
  outline: none;
  transition: all 0.2s;
  font-family: 'Inter', sans-serif;
}

.search-input:focus {
  border-color: #4F46E5;
  box-shadow: 0 0 0 4px rgba(79, 70, 229, 0.1);
}

/* Notifications Dropdown */
.notifications-dropdown {
  min-width: 420px;
}

.notification-item {
  padding: 16px 20px;
  border-bottom: 1px solid #F3F4F6;
  cursor: pointer;
  transition: all 0.2s;
  display: flex;
  gap: 14px;
  align-items: flex-start;
}

.notification-item:last-child {
  border-bottom: none;
}

.notification-item:hover {
  background: #F9FAFB;
}

.notification-item.unread {
  background: #EFF6FF;
}

.notification-item.unread:hover {
  background: #DBEAFE;
}

.notification-icon {
  width: 40px;
  height: 40px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.notification-icon.success {
  background: #D1FAE5;
  color: #059669;
}

.notification-icon.warning {
  background: #FEF3C7;
  color: #D97706;
}

.notification-icon.info {
  background: #DBEAFE;
  color: #2563EB;
}

.notification-content {
  flex: 1;
  min-width: 0;
}

.notification-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 6px;
  gap: 12px;
}

.notification-title {
  font-size: 15px;
  font-weight: 600;
  color: #111827;
  line-height: 1.4;
}

.notification-time {
  font-size: 12px;
  color: #9CA3AF;
  white-space: nowrap;
  flex-shrink: 0;
}

.notification-message {
  font-size: 14px;
  color: #6B7280;
  margin: 0 0 4px 0;
  line-height: 1.5;
}

/* Profile Dropdown */
.profile-dropdown {
  min-width: 280px;
}

.profile-dropdown .profile-info {
  padding: 20px;
  border-bottom: 1px solid #F3F4F6;
  display: flex;
  align-items: center;
  gap: 12px;
}

.profile-dropdown .profile-avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  overflow: hidden;
  flex-shrink: 0;
}

.profile-dropdown .profile-avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.profile-details {
  flex: 1;
  min-width: 0;
}

.profile-details h4 {
  font-size: 15px;
  font-weight: 600;
  color: #111827;
  margin: 0 0 4px 0;
}

.profile-details p {
  font-size: 13px;
  color: #6B7280;
  margin: 0;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.profile-menu {
  padding: 8px 0;
}

.profile-menu-item {
  padding: 12px 20px;
  cursor: pointer;
  transition: all 0.2s;
  font-size: 14px;
  color: #4B5563;
  display: flex;
  align-items: center;
  text-decoration: none;
}

.profile-menu-item:hover {
  background: #F9FAFB;
  color: #4F46E5;
}

.profile-menu-item.danger {
  color: #EF4444;
}

.profile-menu-item.danger:hover {
  background: #FEF2F2;
}

/* Fade Transition */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.2s, transform 0.2s;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>
