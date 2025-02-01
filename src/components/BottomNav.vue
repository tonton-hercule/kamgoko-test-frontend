<template>
  <div class="bottom-nav d-md-none">
    <div class="d-flex justify-content-around align-items-center h-100">
      <button class="nav-btn">
        <i class="bi bi-house"></i>
      </button>
      <button class="nav-btn">
        <i class="bi bi-credit-card"></i>
      </button>
      <button class="nav-btn active btn btn-primary text-white">
        <i class="bi bi-arrow-return-right rotated-icon"></i>
      </button>
      <button class="nav-btn">
        <i class="bi bi-arrow-left-right"></i>
      </button>
      <button class="nav-btn">
        <i class="bi bi-three-dots"></i>
      </button>
    </div>
  </div>
</template>

<style scoped>
.btn-outline-secondary {
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Bottom Navigation (Visible sur Mobile) */
.bottom-nav {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  height: 60px;
  background: white;
  border-top: 1px solid #f0f0f0;
  z-index: 1000;
}

.nav-btn {
  border: none;
  background: none;
  padding: 8px 16px;
  color: #666;
}

.nav-btn.active {
  color: #0066FF;
}

.rotated-icon {
  transform: rotate(-30deg);
  display: inline-block;
}
</style>
