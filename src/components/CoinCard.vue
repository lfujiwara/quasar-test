<template>
  <div class="q-pa-md">
    <q-markup-table v-if="!isFetching">
      <thead>
        <th class="text-left">
          Crypto
        </th>
        <th class="text-left">
          Price
        </th>
        <th class="text-left">
          Market Cap
        </th>
        <th class="text-left">
          24-hour change
        </th>
      </thead>
      <tbody>
        <tr v-for="(row,i) in rows" v-bind:key="i">
          <td class="text-left">
            <img class="vertical-middle" :src="row.iconUrl" style="width: 1.5em"> {{ row.name }}
          </td>
          <td class="text-left">
            $ {{ normalizePrice(row.price) }}
          </td>
          <td class="text-left">
            $ {{ normalizeMarketCap(row.marketCap) }} millions
          </td>
          <td class="text-left" :class="{ 'red-text':(row.change < 0), 'green-text':(row.change > 0) }">
            <q-icon name="keyboard_arrow_up" v-if="isPositive(row.change)"/>
            <q-icon name="keyboard_arrow_down" v-if="isNegative(row.change)"/>
            {{ row.change }} %
          </td>
        </tr>
      </tbody>
    </q-markup-table>
    <q-circular-progress
      v-else
      indeterminate
      size="50px"
      color="primary"
      class="fixed-center"
    />
  </div>
</template>

<style>
.red-text {
  color: red;
}
.green-text {
  color: green;
}
</style>

<script>
export default {
  data: () => ({
    rows: [],
    isFetching: true
  }),
  methods: {
    sleep: (ms) => (new Promise(resolve => setTimeout(resolve, ms))),
    fetchCoins: function () {
      fetch('https://api.coinranking.com/v1/public/coins')
        .then(res => res.json())
        .then(async res => {
          await this.sleep(500)
          let data = res.data
          this.rows = data.coins
          this.isFetching = false
        })
    },
    isPositive: (v) => (v > 0),
    isNegative: (v) => (v < 0),
    normalizePrice: (price) => (Math.round(price * 100) / 100).toString().padEnd(15),
    normalizeMarketCap: (marketCap) => {
      return (Math.round(marketCap / 10000) / 100).toString().padEnd(15)
    }
  },
  created () {
    setTimeout(this.fetchCoins, 5 * 60 * 1000)
    this.fetchCoins()
  },
  beforeMount () {
    this.isFetching = true
  }
}
</script>
