<template>
    <div class="d-flex justify-content-between align-items-center p-3" :class="{'bg-white': isDesktop, 'bg-mobile border-bottom': !isDesktop}">
      <div class="d-flex align-items-center">
        <!-- Bouton de retour -->
        <button class="btn btn-default border me-2 d-none d-md-block">
          <i class="bi bi-chevron-left"></i>
        </button>

        <!-- Bouton de retour pour mobile -->
        <button class="btn btn-link d-md-none" @click="$emit('toggleBack')">
          <i class="bi bi-chevron-left"></i>
        </button>
        
        <!-- Titre en gras -->
        <h5 class="mb-0 ms-2 fw-bold">Account Details</h5>
      </div>
      
      <div class="d-flex align-items-center">
        <!-- Barre de recherche visible uniquement sur desktop -->
        <div class="search-box me-4 position-relative d-none d-md-block">
          <i class="bi bi-search position-absolute search-icon"></i>
          <input type="text" class="form-control ps-5" placeholder="Type to search...">
        </div>
        
        <!-- Icône de notification visible uniquement sur desktop -->
        <div class="notifications me-4 d-none d-md-block">
          <i class="bi bi-bell"></i>
        </div>
        
        <!-- Image de profil -->
        <div class="profile">
          <img src="/images/Black-women-health.webp" alt="Profile" class="rounded-circle">
        </div>
      </div>
    </div>
  </template>
  
  <style scoped>
   
  .bg-mobile {
    background-color: #f1f5f5;
    border-bottom: 1px solid #f0f0f0;
  }
  
  .search-box {
    position: relative;
    width: 300px;
  }
  
  .search-icon {
    left: 15px;
    top: 50%;
    transform: translateY(-50%);
    color: #666;
  }
  
  .form-control {
    border-radius: 20px;
    border: 1px solid #f0f0f0;
    background-color: #f8f9fa;
  }
  
  .form-control:focus {
    box-shadow: none;
    border-color: #0066FF;
  }
  
  .notifications {
    color: #666;
    cursor: pointer;
  }
  
  .profile img {
    width: 32px;
    height: 32px;
    cursor: pointer;
  }
  </style>
  
  <script setup>
  import { ref, onMounted, onBeforeUnmount } from 'vue';
  
  const isDesktop = ref(window.innerWidth >= 768);
  
  const checkScreenSize = () => {
    isDesktop.value = window.innerWidth >= 768;
  };
  
  onMounted(() => {
    window.addEventListener('resize', checkScreenSize);
  });
  
  onBeforeUnmount(() => {
    window.removeEventListener('resize', checkScreenSize);
  });
  </script>
  