<template>
  <div class="q-pa-md">
    <q-markup-table>
      <thead>
        <th class="text-left">
          Crypto
        </th>
        <th class="text-right">
          Price
        </th>
        <th class="text-right">
          Market Cap
        </th>
        <th class="text-right">
          24-hour change
        </th>
      </thead>
      <tbody>
        <tr v-for="(row,i) in rows" v-bind:key="i">
          <td class="text-left">
            <img class="vertical-middle" :src="row.iconUrl" style="width: 1.5em"> {{ row.name }}
          </td>
          <td class="text-right">
            $ {{ Math.round(row.price*100)/100 }}
          </td>
          <td class="text-right">
            $ {{ Math.round(row.marketCap/10000)/100 }} millions
          </td>
          <td class="text-right" :class="{ 'red-text':(row.change < 0), 'green-text':(row.change > 0) }">
            {{ row.change }} %
          </td>
        </tr>
      </tbody>
    </q-markup-table>
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
    fetchCoins: function () {
      this.isFetching = true
      fetch('https://api.coinranking.com/v1/public/coins')
        .then(res => res.json())
        .then(res => {
          let data = res.data
          this.rows = data.coins
          this.isFetching = false
        })
      console.log(this.rows)
    }
  },
  created () {
    setTimeout(this.fetchCoins, 5 * 60 * 1000)
    this.fetchCoins()
  }
}
</script>
