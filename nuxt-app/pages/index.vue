<template>
  <div class="max-w-dvw mx-auto px-32 py-8 bg-background-dark text-text-primary">
    <h1 class="text-3xl font-bold mb-6 text-bitcoin-gold">График цен Bitcoin</h1>

    <PeriodSelector :period="period" @update:period="period = $event" />

    <DateRangePicker v-if="period === 'custom'" v-model="customRange" />

    <div v-if="error" class="text-center text-red-500">{{ error }}</div>
    <PriceChart v-else :data="data" />
    <p class="mt-16 text-bitcoin-gold-secondary">
      Данные получены с
      <a
        class="hover:text-bitcoin-gold"
        href="https://developers.binance.com/docs/binance-spot-api-docs/rest-api/market-data-endpoints"
        >API Binance</a
      >
    </p>
    <div v-if="loading" class="text-center text-text-secondary">Загрузка…</div>
  </div>
</template>

<script setup lang="ts">
import DateRangePicker from '~/components/DateRangePicker.vue';
import PeriodSelector from '~/components/PeriodSelector.vue';
import PriceChart from '~/components/PriceChart.vue';
import { usePrices, type UsePrices } from '~/composables/use-prices.composable';

const { period, customRange, data, loading, error }: UsePrices = usePrices();
</script>
