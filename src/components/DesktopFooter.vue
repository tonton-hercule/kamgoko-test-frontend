<template>
  <footer class="footer d-none d-md-flex justify-content-between align-items-center px-4 py-3">
    <div class="footer-links d-flex gap-3">
      <a href="#" class="fw-bold">Privacy Policy</a>
      <a href="#" class="fw-bold">License</a>
      <a href="#" class="fw-bold">API</a>
      <a href="#" class="fw-bold">Help Center</a>
      <span>© {{ currentYear }} All rights reserved</span>
    </div>

    <div class="footer-settings d-flex align-items-center gap-3">
      <div class="language-selector d-flex align-items-center">
        <span class="fw-bold">English</span>
        <i class="bi bi-globe ms-1"></i>
      </div>

      <button class="btn btn-outline-secondary rounded-circle" @click="toggleDarkMode">
        <i :class="darkMode ? 'bi bi-brightness-high' : 'bi bi-moon'"></i>
      </button>
    </div>
  </footer>

  <!-- Bottom Navigation pour Mobile -->
  <BottomNav />
</template>

<script setup>
import { ref, onMounted } from 'vue';
import BottomNav from './BottomNav.vue';

const currentYear = new Date().getFullYear();
const darkMode = ref(false);

const toggleDarkMode = () => {
  darkMode.value = !darkMode.value;
  document.body.classList.toggle('dark-mode', darkMode.value);
};

onMounted(() => {
  darkMode.value = document.body.classList.contains('dark-mode');
});
</script>

<style scoped>
/* Footer (Visible sur Desktop) */
.footer {
  border-top: 2px solid #e0e0e0;
  background-color: #fff;
}

.footer-links a {
  text-decoration: none;
  color: black;
}

.footer-links a:hover {
  text-decoration: underline;
}

.language-selector {
  cursor: pointer;
}

.btn-outline-secondary {
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
}

</style>
