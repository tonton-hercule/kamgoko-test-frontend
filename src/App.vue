<template>
  <div class="app-container d-flex">
    <Sidebar class="d-none d-md-block" />

    <div class="flex-grow-1 container" :class="{ 'main-content': !isDesktop }">
      <Topbar />

      <!-- Main Section -->
      <div class="px-4 pt-4">
        <!-- Balance Section -->
        <div class="mb-4">
          <div class="balance-amount">$120,420.50</div>
          <div class="text-muted small">Account **** 4567</div>
        </div>

        <!-- Actions Section -->
        <div
          class="d-flex justify-content-between align-items-center mb-4 border-bottom pb-3 d-none d-md-flex"
        >
          <div class="d-flex">
            <template v-for="action in actions" :key="action.label">
              <button class="btn btn-action me-4">
                <i :class="action.icon" class="me-2"></i>
                {{ action.label }}
              </button>
            </template>
          </div>
          <div class="d-flex align-items-center">
            <button class="btn btn-action me-3">
              <i class="bi bi-search"></i>
              Search
            </button>
            <button class="btn btn-action">
              <i class="bi bi-calendar3"></i>
              August 2022
            </button>
          </div>
        </div>

        <!-- Mobile View: Linked Card First -->
        <div v-if="!isDesktop" class="row mb-4 py-3">
          <div class="col-md-12">
            <!-- Linked Card -->
            <div class="bg-white p-3 rounded-3">
              <div class="d-flex align-items-center">
                <div class="card-gradient me-3"></div>
                <div>
                  <div class="fw-bold">Visa Gold Paywave</div>
                  <div class="d-flex justify-content-between align-items-center">
                    <span class="text-muted">**** 8790</span>
                    <span class="text-muted ms-4 d-none d-md-block">03/22</span>
                  </div>
                </div>
              </div>
              <hr />
              <div class="fw-bold text-center">
                <SlidingAccountDetails />
              </div>
            </div>
          </div>
        </div>

        <!-- Transactions Section -->
        <div class="row mb-5 mb-md-0">
          <div class="col-md-8">
            <h1 class="d-md-none latest-transactions-title fw-bold">Latest Transactions</h1>

            <div class="transactions-section flex-grow-1">
              <template v-for="(group, date) in groupedTransactions" :key="date">
                <div class="mb-4">
                  <div class="text-muted mb-3">{{ date }}</div>
                  <div class="transactions">
                    <template v-for="(transaction, index) in group" :key="transaction.id">
                      <div
                        class="transaction-item d-flex justify-content-between align-items-center py-2 mb-2"
                        :class="{
                          'border-bottom': isDesktop && index !== group.length - 1,
                          'bg-white rounded-2 px-2': !isDesktop,
                        }"
                      >
                        <div class="d-flex">
                          <div class="transaction-icon me-3">
                            <div class="checker-icon rounded-4"></div>
                          </div>
                          <div>
                            <div class="transaction-title fw-bold">{{ transaction.title }}</div>
                            <div class="text-muted small">{{ transaction.time }}</div>
                          </div>
                        </div>
                        <div class="fw-bold small text-end amount-text">
                          {{ formatAmount(transaction.amount) }}
                        </div>
                      </div>
                    </template>
                  </div>
                </div>
              </template>
            </div>
          </div>

          <div v-if="isDesktop" class="col-md-4">
            <!-- Right Section -->
            <div class="ms-4">
              <!-- Linked Card -->
              <div class="bg-light p-3 rounded-3">
                <div class="text-muted mb-3 d-none d-md-block">Linked Card</div>
                <div class="d-flex align-items-center">
                  <div class="card-gradient me-3"></div>
                  <div>
                    <div class="fw-bold">Visa Gold Paywave</div>
                    <div class="d-flex justify-content-between align-items-center">
                      <span class="text-muted">**** 8790</span>
                      <span class="text-muted ms-4 d-none d-md-block">03/22</span>
                    </div>
                  </div>
                </div>
              </div>

              <!-- Account Details -->
              <div class="mt-4 d-none d-md-block">
                <div class="mb-3">Account Details</div>
                <div class="border rounded-3 p-3">
                  <template v-for="(detail, index) in accountDetails" :key="detail.label">
                    <div
                      :class="[
                        'd-flex',
                        'justify-content-between',
                        'py-2',
                        index !== accountDetails.length - 1 ? 'border-bottom' : '',
                      ]"
                    >
                      <span class="text-muted">{{ detail.label }}</span>
                      <span class="fw-bold">{{ detail.value }}</span>
                    </div>
                  </template>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <DesktopFooter />
    </div>
  </div>
</template>

<script setup>
import Sidebar from '@/components/SideBar.vue'
import Topbar from '@/components/TopBar.vue'
import DesktopFooter from '@/components/DesktopFooter.vue'
import { ref } from 'vue'
import { onMounted } from 'vue'
import { onBeforeUnmount } from 'vue'
import SlidingAccountDetails from '@/components/SlidingAccountDetails.vue'

const actions = [
  { icon: 'bi bi-arrow-left-right', label: 'Transfer' },
  { icon: 'bi bi-credit-card-2-front', label: 'Make a Payment' },
  { icon: 'bi bi-arrow-repeat', label: 'Convert' },
  { icon: 'bi bi-box-arrow-up-right', label: 'Request' },
]

const groupedTransactions = {
  '28 August': [
    { id: 1, title: 'Online purchase at Ebay.com', time: '28 Aug, 3:00 PM', amount: -10480.0 },
    { id: 2, title: 'ATM Cash withdrawal', time: '28 Aug, 2:15 AM', amount: -201.5 },
    { id: 3, title: 'Online purchase on Amazon.com', time: '28 Aug, 5:40 PM', amount: -184.0 },
  ],
  '24 August': [
    { id: 4, title: 'Income payment for projects', time: '24 Aug, 6:20 PM', amount: 3000.0 },
    { id: 5, title: 'Groceries store', time: '24 Aug, 1:00 AM', amount: -400.0 },
    { id: 6, title: 'Monthly home rent', time: '24 Aug, 1:00 AM', amount: -400.0 },
    //{ id: 7, title: 'Online purchase at Ebay.com', time: '19 Aug, 3:10 PM', amount: -396.0 },
    //{ id: 8, title: 'IOfinance UI kit purchase', time: '19 Aug, 4:20 AM', amount: -28.0 },
  ],
}

const accountDetails = [
  { label: 'Account name', value: 'Premium Account' },
  { label: 'Account number', value: 'UK64CT0000010034567' },
  { label: 'Account type', value: 'Single Currency' },
  { label: 'Bonus programm', value: 'Premium' },
  { label: 'Insurance', value: 'Enabled' },
]

const formatAmount = (amount) => {
  const prefix = amount >= 0 ? '+ ' : '- '
  return `${prefix}$${Math.abs(amount).toFixed(2)}`
}

const isDesktop = ref(window.innerWidth >= 768)

const checkScreenSize = () => {
  isDesktop.value = window.innerWidth >= 768
}

onMounted(() => {
  window.addEventListener('resize', checkScreenSize)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', checkScreenSize)
})
</script>

<style scoped>
.main-content {
  background: #f1f5f5;
}

.balance-amount {
  font-size: 32px;
  font-weight: 600;
  line-height: 1.2;
}

.btn-action {
  padding: 8px 12px;
  border: none;
  background: transparent;
  font-size: 14px;
  color: #333;
  font-weight: 600;
}

.btn-action:hover {
  background: #f5f5f5;
  border-radius: 4px;
}

.checker-icon {
  width: 24px;
  height: 24px;
  background: linear-gradient(45deg, #000 25%, transparent 25%),
    linear-gradient(-45deg, #000 25%, transparent 25%),
    linear-gradient(45deg, transparent 75%, #000 75%),
    linear-gradient(-45deg, transparent 75%, #000 75%);
  background-size: 4px 4px;
  background-position:
    0 0,
    0 2px,
    2px -2px,
    -2px 0px;
  border-radius: 4px;
}

.card-gradient {
  width: 48px;
  height: 48px;
  background: linear-gradient(135deg, #2193b0, #6dd5ed);
  border-radius: 8px;
}

.transaction-title {
  font-size: 14px;
  font-weight: 500;
}

.transaction-item:hover {
  background-color: #f8f9fa;
  border-radius: 4px;
}

@media (max-width: 768px) {
  .transactions-section {
    width: 100%;
  }

  .btn-action {
    width: calc(50% - 8px);
    margin-bottom: 8px;
  }
}

/* Empêche le retour à la ligne des montants et Ajuste la largeur au contenu  */
.amount-text {
  white-space: nowrap; 
  min-width: fit-content; 
}

</style>
