<template>
  <div>
    <!-- Trigger button -->
    <button @click="showModal = true" class="btn text-dark px-0 py-2 fw-bold">
      <i class="me-2 bi bi-receipt-cutoff"></i>
      See account details
    </button>

    <!-- Modal Overlay -->
    <Transition name="fade">
      <div v-if="showModal" class="modal-overlay" @click="showModal = false"></div>
    </Transition>

    <!-- Sliding Modal -->
    <Transition name="slide">
      <div v-if="showModal" class="modal-content">
        <!-- Modal Header -->
        <button @click="showModal = false" class="text-center separator mt-4">&nbsp;</button>
        <div
          class="modal-header d-flex justify-content-between align-items-center p-4 border-bottom"
        >
          <h6 class="mb-0 fw-bold">Account Details</h6>
        </div>

        <!-- Modal Body -->
        <div class="modal-body p-4">
          <div
            v-for="detail in accountDetails"
            :key="detail.label"
            class="detail-item d-flex justify-content-between py-3 border-bottom"
          >
            <span class="text-muted">{{ detail.label }}</span>
            <span class="fw-medium">{{ detail.value }}</span>
          </div>
          <div class="py-4">
            <div class="border p-2 rounded-3">
              <i class="bi bi-arrow-clockwise me-2"></i>Update your details
            </div>
          </div>
        </div>
      </div>
    </Transition>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const showModal = ref(false)

const accountDetails = [
  { label: 'Account name', value: 'Premium Account' },
  { label: 'Account number', value: 'UK64CT0000010034567' },
  { label: 'Account type', value: 'Single Currency' },
  { label: 'Bonus programm', value: 'Premium' },
  { label: 'Insurance', value: 'Enabled' },
]
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 1000;
}

.modal-content {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  background: white;
  border-top-left-radius: 16px;
  border-top-right-radius: 16px;
  z-index: 1001;
  max-height: 80vh;
  overflow-y: auto;
}

/* Fade animation for overlay */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* Slide animation for modal */
.slide-enter-active,
.slide-leave-active {
  transition: transform 0.3s ease-out;
}

.slide-enter-from,
.slide-leave-to {
  transform: translateY(100%);
}

.detail-item:last-child {
  border-bottom: none !important;
}

/* Style personnalisé pour le scrollbar */
.modal-content::-webkit-scrollbar {
  width: 4px;
}

.modal-content::-webkit-scrollbar-track {
  background: #f1f1f1;
}

.modal-content::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 2px;
}

.separator {
  width: 50px;
  height: 4px; /* Épaisseur du trait */
  background-color: #ccc; /* Gris clair */
  border-radius: 2px; /* Bords arrondis */
  margin: 8px auto; /* Centrage horizontal */
}
</style>
