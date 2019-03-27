<template>
  <v-flex
    class=" pr-3 pb-3"
    xs12
    md6
    lg4
  >
    <v-card class="green lighten-1 white--text">
      <v-card-title class="headline">
        <strong>{{stock.name}}</strong> <small> (Preço: {{ stock.price | currency}})</small>
      </v-card-title>

    </v-card>
    <v-card>
      <v-container fill-height>
        <v-text-field
          :error="quantity < 0 || !Number.isInteger(quantity) || inssuficientFunds"
          label="Quantidade"
          type="number"
          v-model.number="quantity"
        ></v-text-field>
        <v-btn
          color="green lighten-1 white--text"
          @click="buyStock"
          :disabled="quantity <= 0 || !Number.isInteger(quantity) || inssuficientFunds"
        >{{ inssuficientFunds ? 'Insuficiente' : 'Comprar' }}</v-btn>
      </v-container>
    </v-card>
  </v-flex>
</template>

<script>
export default {
  props: ['stock'],
  data () {
    return {
      quantity: 0
    }
  },
  computed: {
    funds(){
      return this.$store.getters.funds
    },
    inssuficientFunds(){
      return this.quantity * this.stock.price > this.funds
    }
  },
  methods: {
    buyStock () {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity,

      }
      // eslint-disable-next-line no-console
      this.$store.dispatch('buyStocks', order)
      this.quantity = 0
    }
  },
}
</script>

<style>
</style>
