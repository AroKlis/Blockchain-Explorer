<template>
  <div id="app">
    <header>
      <img src="https://xe.network/assets/logo.svg"/>
    </header>
    <body>
      <div class="search-box">
        <p>Search the Xi Blockchain</p>
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Search..."
          v-model="query"
        />
      </div>
      <div class = "search-result">
        
      </div>
      <div class = "block-count">
        <p> Current Block Count</p>
        <p class = "number of blocks">{{blockchain[0].height}}</p>
      </div>
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
    }
  },

  mounted(){
    fetch(`${this.api_url}`)
      .then(res => res.json())
      .then(data => this.blockchain = data)
      .catch(err => console.log(err.message))
  },


    
  }

</script>

<style>


#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

html{
  padding: 0;
  margin: 0;
  border: 0;
  background-color: rgba(0, 0, 0, 0.2);

}

header{
  margin:0;
  padding: 0;
  background-color: rgba(0, 0, 0, 0.9);
}

body {
  background-color: rgba(255, 255, 255, 0.1);
  margin:0px;
  padding: 0px;
  font-family: system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial,sans-serif,Apple Color Emoji,Segoe UI Emoji;
}

.search-box{
  background-color: rgba(0, 0, 0, 0.80);
  padding: 2.6rem;
  border: 0px;
  margin: 0px;
  color: white;
  text-align: left;
  display: block;
  padding-left: 1rem;
  }
.search-box p{
  font-size: 2em;
  margin: 0%;
}
.search-bar{
  width: 80%;
  height: 3em;
  border-radius: 5px;
  
}

.tabel-header{
  width: 30%;
  font-size: 1.5em;  
}

.block-count p{
  color: rgb(33, 216, 33);
  font-weight: 500;
  font-size: 1.2em;
  background-color: rgba(255, 255, 255, 0.9);
  margin: auto;
  width: 20%;
  text-align: center;
  
}

</style>


