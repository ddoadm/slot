<template>
  <div id="app">
    <h3 class="header-text">Pragmatic Play Slot Demo</h3>
    <div class="header-input">
      <vs-input icon="search" label="Search" placeholder="Search" v-model="search"/>
      <vs-select
      class="currency"
      label="Currency"
      v-model="currency"
      >
        <vs-select-item :key="index" :value="item.code" :text="[item.code, item.currency].join(' - ')" v-for="item,index in currencies" />
      </vs-select>
    </div>

    <div class="game-list" v-if="!gameSelected">
      <vs-row vs-justify="center">
        <vs-col class="game" v-for="g in gameStructure.games" type="flex" vs-justify="center" vs-align="center" vs-lg="3" vs-sm="4" vs-xs="6">
          <vs-card class="cardx" fixedHeight>
            <div slot="header">
              <h3 v-html="g.name"></h3>
            </div>
            <div slot="media">
              <img :src="g.img">
            </div>
            <div slot="footer">
              <vs-row vs-justify="flex-end">
                <vs-chip color="danger" style="min-width: 60px;">
                  <b>RTP {{g.rtp}}</b>
                </vs-chip>
                <vs-button v-if="g.ready" color="primary" icon="play_arrow">
                  <b>Play</b>
                </vs-button>
                <vs-chip v-else color="warning" style="min-width: 60px;">
                  <b>Coming Soon</b>
                </vs-chip>
              </vs-row>
            </div>
          </vs-card>
        </vs-col>
      </vs-row>
      <!-- {{gameStructure}} -->
    </div>
  </div>
</template>

<style>
  #app {
    width: 100%;
    height: 100vh;
    font-family: Poppins,-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen,Ubuntu,Cantarell,Fira Sans,Droid Sans,Helvetica Neue,sans-serif;
    color: #333;
    background-color: #f5f5f5;
  }

  .header-input {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .header-input > div {
    margin-left: 10px;
    margin-right: 10px;
  }
  .header-text {
    text-align: center;
    padding-top:10px;
    padding-bottom: 10px;
  }
  .game {
    padding: 8px;
  }
</style>

<script>
  import currencyData from 'currency-codes/data'
  import gameStructure from './data/games.json'

  export default {
    data: () => ({
      search: '',
      currencies: currencyData,
      currency: 'IDR',
      gameStructure: gameStructure,
      gameSelected: ''
    })
  }
</script>
