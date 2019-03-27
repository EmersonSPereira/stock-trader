<template>
  <v-toolbar>
    <v-toolbar-title class="headline text-uppercase mr-4"><span>Stock</span>
      <span class="font-weight-light">Trader</span></v-toolbar-title>
    <v-spacer></v-spacer>
    <v-toolbar-items class="hidden-sm-and-down">
      <v-btn
        flat
        to="/"
      >Ínicio</v-btn>
      <v-btn
        flat
        to="/portfolio"
      >Portifólio</v-btn>
      <v-btn
        flat
        to="/stocks"
      >Ações</v-btn>
      <v-btn
        flat
        to=""
        @click="endDay"
      >Finalizar dia</v-btn>
      <v-spacer></v-spacer>
      <v-menu offset-y>
        <v-btn
          flat
          slot="activator"
        >Salvar & Carregar</v-btn>
        <v-list>
          <v-list-tile @click="saveData">
            <v-list-tile-title>Salvar dados</v-list-tile-title>
          </v-list-tile>
          <v-list-tile @click="loadDataLocal">
            <v-list-tile-title>Carregar dados</v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-menu>
      <v-layout align-center>
        <span class="text-uppercase grey--text text--darken-2">
          Saldo: {{ funds | currency}}
        </span>
      </v-layout>
    </v-toolbar-items>
    <v-menu class="hidden-md-and-up">
      <v-toolbar-side-icon slot="activator"></v-toolbar-side-icon>
      <v-list>
        <v-list-tile to="/">
          <v-list-tile-title>Ínicio</v-list-tile-title>
        </v-list-tile>
        <v-list-tile to="/portfolio">
          <v-list-tile-title>Portifólio</v-list-tile-title>
        </v-list-tile>
        <v-list-tile to="/stocks">
          <v-list-tile-title>Ações</v-list-tile-title>
        </v-list-tile>
        <v-list-tile @click="endDay">
          <v-list-tile-title>Finalizar dia</v-list-tile-title>
        </v-list-tile>
        <v-list-tile @click="saveData">
          <v-list-tile-title>Salvar dados</v-list-tile-title>
        </v-list-tile>
        <v-list-tile @click="loadDataLocal">
          <v-list-tile-title>Carregar dados</v-list-tile-title>
        </v-list-tile>
        <v-divider class="dark"/>
        <v-list-tile class="green darken-4">
        <span class="text-uppercase white--text text--darken-4">
          Saldo: {{ funds | currency}}
        </span>
        </v-list-tile>
      
        
      </v-list>
    </v-menu>
  </v-toolbar>

</template>

<script>
import { mapActions } from 'vuex'
export default {
  computed: {
    funds(){
      return this.$store.getters.funds
    }
  },
  methods: {
    ...mapActions(['randomizeStocks', 'loadData']),
    endDay(){
      this.randomizeStocks()
    },
    saveData(){
      const { funds, stockPortfolio, stocks } = this.$store.getters
      this.$http.put('data.json', { funds, stockPortfolio, stocks })
    },
    loadDataLocal(){
      this.loadData()
    }
}
}
</script>

<style>
</style>
