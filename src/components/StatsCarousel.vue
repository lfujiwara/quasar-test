<template>
  <div class="row">
    <q-carousel
        v-model="slide"
        transition-prev="scale"
        transition-next="scale"
        swipeable
        animated
        control-color="white"
        navigation
        padding
        arrows
        height="300px"
        class="bg-primary text-white shadow-1 rounded-borders col-12"
      >
        <q-carousel-slide
          v-for="stat in stats"
          :key="stat.title"
          :name="stat.title"
          class="column no-wrap flex-center"
        >
          <q-icon :name="stat.icon" size="56px" />
          <div class="text-bold">
            {{ stat.title }}
          </div>
          <div class="q-mt-md text-center">
            {{ stat.data }}
          </div>
        </q-carousel-slide>
      </q-carousel>
  </div>
</template>

<style>
.w-full {
  width: 100vw;
}
</style>

<script>
export default {
  data: () => ({
    stats: null,
    slide: 'Total trade volume in 24 hours'
  }),
  created () {
    fetch('https://api.coinranking.com/v1/public/stats')
      .then(res => res.json())
      .then(res => {
        this.stats = [
          {
            title: 'Total trade volume in 24 hours',
            data: (Math.round(res.data.total24hVolume / 10000000) / 100).toString() + ' billions',
            icon: 'loop'
          },
          {
            title: 'Total number of coins',
            data: res.data.totalCoins,
            icon: 'call_split'
          },
          {
            title: 'Total amount of markets used for price calculation',
            data: res.data.totalMarkets,
            icon: 'local_mall'
          },
          {
            title: 'Total amount of exchanges paired with Coinranking',
            data: res.data.totalExchanges,
            icon: 'poll'
          },
          {
            title: 'Market capitalization. Price times circulating supply',
            data: (Math.round(res.data.totalMarketCap / 10000000) / 100).toString() + ' billions',
            icon: 'attach_money'
          }
        ]
      })
  }
}
</script>
