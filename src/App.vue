<template>
  <div id="app">

    <header>
      <img src="https://xe.network/assets/logo.svg"/>
    </header>

    <body>

      <!-- Search box -->
      <div class="search-box">
        <p>Search the Xi Blockchain</p>
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Enter the height, timestamp or hash..."
          v-model="query"
        />
        <button @click="search()"><i class="fas fa-search"></i></button>
      </div>

      <!-- Displays additional information of the block requested -->
      <div class = "search-result">
        <div v-if="result === 0">
          Search results
        </div>

        <div v-else>
          <span> Block Height: {{result[0].height}} </span>
          <span> Timestamp: {{result[0].timestamp}} </span>
          <span> Miner: {{result[0].miner}} </span>
          <span> Leadger Hash: {{result[0].ledgerHash}} </span>
          <span> Parent Hash: {{result[0].parentHash}} </span>
          <span> Hash: {{result[0].hash}} </span> 
        </div>
      </div>

      <!-- Displays the height number of the latest block -->
      <div class = "block-count">
        <p> Current Block Count</p>
        <p class = "number of blocks">{{blockchain[0].height}}</p>
      </div>

      <!-- Displays a tabel of the blocks in the blockchain -->
      <table class="blockchain-tabel">
        <tr>
          <th class = "tabel-header">Block Height</th>
          <th class = "tabel-header">Timestamp</th>
          <th class = "tabel-header">Number of Transactions</th>
          <th class = "tabel-header">Hash</th>
        </tr>

        <tr v-for="block in blockchain" :key="block.height" >
          <td>{{ block.height }}</td>
          <td>{{ block.timestamp }}</td>
          <td>{{ block.transactions.length }}</td>
          <td>{{ block.hash }}</td>
        </tr>   
      </table>
      
    </body>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      api_url: 'https://xi.test.network/blocks',
      query: '',
      blockNumber: {},
      address: {},
      hash: {},
      timestamp: {},
      height: {},
      blockchain: {},
      result:{}
    }
  },

  // Fetches data from the API when website is rendered
  mounted(){

    fetch(`${this.api_url}`)
      .then(res => res.json())
      .then(data => this.blockchain = data)
      .catch(err => console.log(err.message))
      this.result = 0
      
  },

  // Searches for the block with the requested Height, Timestamp or Hash
  methods: {

    search(){
      this.result = this.blockchain.filter( x=>((x.height == this.query)    ||
                                                (x.timestamp == this.query) ||
                                                (x.hash == this.query)))

    }   
  
  }
}
  
    

</script>

<style>

  @import'/assets/stylesheet.css';

</style>