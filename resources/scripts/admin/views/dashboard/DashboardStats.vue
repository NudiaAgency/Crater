<template>
  <div class="grid gap-6 sm:grid-cols-2 lg:grid-cols-9 xl:gap-8">
    <!-- Amount Due -->
    <DashboardStatsItem
      :icon-component="DollarIcon"
      :loading="!dashboardStore.isDashboardDataLoaded"
      :route="
        userStore.hasAbilities(abilities.VIEW_INVOICE) ? `/admin/invoices` : ''
      "
      :large="true"
      :label="$t('dashboard.cards.due_amount')"
    >
      <BaseFormatMoney
        :amount="dashboardStore.stats.totalAmountDue"
        :currency="companyStore.selectedCompanyCurrency"
      />
    </DashboardStatsItem>

    <!-- Customers -->
    <DashboardStatsItem
      :icon-component="CustomerIcon"
      :loading="!dashboardStore.isDashboardDataLoaded"
      :route="
        userStore.hasAbilities(abilities.VIEW_CUSTOMER)
          ? `/admin/customers`
          : ''
      "
      :label="$t('dashboard.cards.customers')"
    >
      {{ dashboardStore.stats.totalCustomerCount }}
    </DashboardStatsItem>

    <!-- Invoices -->
    <DashboardStatsItem
      :icon-component="InvoiceIcon"
      :loading="!dashboardStore.isDashboardDataLoaded"
      :route="
        userStore.hasAbilities(abilities.VIEW_INVOICE) ? `/admin/invoices` : ''
      "
      :label="$t('dashboard.cards.invoices')"
    >
      {{ dashboardStore.stats.totalInvoiceCount }}
    </DashboardStatsItem>

    <!-- Estimates -->
    <DashboardStatsItem
      :icon-component="EstimateIcon"
      :loading="!dashboardStore.isDashboardDataLoaded"
      :route="
        userStore.hasAbilities(abilities.VIEW_ESTIMATE)
          ? `/admin/estimates`
          : ''
      "
      :label="$t('dashboard.cards.estimates')"
    >
      {{ dashboardStore.stats.totalEstimateCount }}
    </DashboardStatsItem>
  </div>
</template>

<script setup>
import DollarIcon from '@/scripts/components/icons/dashboard/DollarIcon.vue'
import CustomerIcon from '@/scripts/components/icons/dashboard/CustomerIcon.vue'
import InvoiceIcon from '@/scripts/components/icons/dashboard/InvoiceIcon.vue'
import EstimateIcon from '@/scripts/components/icons/dashboard/EstimateIcon.vue'
import abilities from '@/scripts/admin/stub/abilities'
import DashboardStatsItem from './DashboardStatsItem.vue'

import { inject } from 'vue'
import { useDashboardStore } from '@/scripts/admin/stores/dashboard'
import { useCompanyStore } from '@/scripts/admin/stores/company'
import { useUserStore } from '@/scripts/admin/stores/user'

const utils = inject('utils')

const dashboardStore = useDashboardStore()
const companyStore = useCompanyStore()
const userStore = useUserStore()
</script>
