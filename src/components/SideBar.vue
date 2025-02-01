<template>
    <div class="sidebar d-flex flex-column h-100">
      <div class="logo p-4">
        <div class="p-logo rounded-5 h3">P</div>
      </div>
      
      <div class="navigation-section px-4">
        <p class="text-muted small mb-2">Navigation</p>
        <div class="nav-items">
          <div class="nav-item d-flex align-items-center mb-2" :class="{ active: currentRoute === 'dashboard' }">
            <i class="bi bi-grid me-2"></i>
            <span>Dashboard</span>
          </div>
          <div class="nav-item d-flex align-items-center mb-2 active">
            <i class="bi bi-credit-card me-2"></i>
            <span>Accounts</span>
          </div>
          <div class="nav-item d-flex align-items-center mb-2">
            <i class="bi bi-credit-card me-2"></i>
            <span>Cards</span>
          </div>
          <div class="nav-item d-flex align-items-center mb-2">
            <i class="bi bi-arrow-left-right me-2"></i>
            <span>Transactions</span>
          </div>
          <div class="nav-item d-flex align-items-center mb-2">
            <i class="bi bi-arrow-return-right rotated-icon me-2"></i>
            <span>Payment</span>
          </div>
          <div class="nav-item d-flex align-items-center mb-2">
            <i class="bi bi-file-text me-2"></i>
            <span>Invoicing</span>
          </div>
          <div class="nav-item d-flex align-items-center mb-2">
            <i class="bi bi-graph-up me-2"></i>
            <span>Trading</span>
          </div>
          <div class="nav-item d-flex align-items-center mb-2">
            <i class="bi bi-bar-chart-fill me-2"></i>
            <span>Reports</span>
          </div>
        </div>
      </div>
  
      <div class="balances-section px-4 mt-4">
        <p class="text-muted small mb-2">Balances</p>
        <div class="balance-items">
          <div class="balance-item d-flex align-items-center mb-2">
            <span class="currency-flag me-2"><img src="/images/us.png" alt="US"></span>
            <span>100,050.75 USD</span>
          </div>
          <div class="balance-item d-flex align-items-center mb-2">
            <span class="currency-flag me-2"><img src="/images/eu.png" alt="EU"></span>
            <span>2,310.40 EUR</span>
          </div>
          <div class="balance-item d-flex align-items-center mb-2">
            <span class="currency-flag me-2"><img src="/images/gb.png" alt="GB"></span>
            <span>9455.50 GBP</span>
          </div>
        </div>
      </div>
  
      <div class="mt-auto p-4">
        <span class="w-100 text-start">
          <i class="bi bi-plus-circle me-2"></i>
          Open a balance
        </span>
        
        <div class="nav-item d-flex align-items-center mt-3">
          <i class="bi bi-gear me-2"></i>
          <span>Profile Settings</span>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const currentRoute = ref('accounts')
  </script>
  
  <style scoped>
  .sidebar {
    width: 250px;
    background-color: #f1f5f5;
  }
  
  .p-logo {
    width: 32px;
    height: 32px;
    background-color: #0066FF;
    color: white;
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
  }
  
  .nav-item {
    color: #666;
    padding: 8px;
    border-radius: 8px;
    cursor: pointer;
  }
  
  .nav-item:hover, .nav-item.active {
    background-color: #f5f5f5;
  }
  
  .balance-item {
    font-size: 0.9rem;
    color: #333;
  }
  
  .currency-flag {
    font-size: 1.2rem;
  }

  .currency-flag img {
    width: 22px;
    height: 22px;
    cursor: pointer;
  }

  .rotated-icon {
  transform: rotate(-30deg);
  display: inline-block;
}
  </style>
  