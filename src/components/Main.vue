<template>
  <div>
    <md-table>
      <md-table-toolbar>
        <h1 class="md-title">Popular Currencies</h1>
      </md-table-toolbar>

      <md-table-row>
        <md-table-head>Logo</md-table-head>
        <md-table-head>Full Name</md-table-head>
        <md-table-head>Short Name</md-table-head>
        <md-table-head>Price</md-table-head>
        <md-table-head>Supply</md-table-head>
      </md-table-row>

      <md-table-row md-table v-bind:key="item.id" v-for="item in sortedData(data)">
        <md-table-cell md-label="Logo"><img width="55" v-bind:src="URL + item.CoinInfo.ImageUrl" v-bind:alt:="item.CoinInfo.FullName"></md-table-cell>
        <md-table-cell>{{item.CoinInfo.FullName}}</md-table-cell>
        <md-table-cell>{{item.CoinInfo.Name}}</md-table-cell>
        <md-table-cell>{{item.RAW.USD.PRICE}}</md-table-cell>
        <md-table-cell>{{item.RAW.USD.SUPPLY}}</md-table-cell>
      </md-table-row>
    </md-table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Main',
  data () {
    return {
      URL: 'https://www.cryptocompare.com',
      API_BASE: 'https://min-api.cryptocompare.com',
      data: [],
      update: null
    }
    console.log(data)
  },
  mounted() {
    this.fetchData()
    this.update = setInterval(this.fetchData, 300000)
  },
  methods: {
    fetchData: function() {
      axios.get(`${this.API_BASE}/data/top/mktcapfull?limit=20&tsym=USD`)
      .then(response => {
        this.data = response.data.Data 
        console.log(response)
        console.log('Update', new Date())
        })
    },
    sortedData: function(array) {
      return array.slice().sort(function(a, b) {
        return b.RAW.USD.PRICE - a.RAW.USD.PRICE
      })
    }
  }
}
</script>
