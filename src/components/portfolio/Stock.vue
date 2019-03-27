<template>
  <v-flex
    class=" pr-3 pb-3"
    xs12
    md6
    lg4
  >
    <v-card class="blue lighten-1 white--text">
      <v-card-title class="headline">
        <strong>{{stock.name}}</strong>
        <small>
          (Preço: {{ stock.price | currency}} | Qtde: {{ stock.quantity }})
        </small>
      </v-card-title>

    </v-card>
    <v-card>
      <v-container fill-height>
        <v-text-field
          label="Quantidade"
          type="number"
          v-model.number="quantity"
          :error="quantity < 0 || !Number.isInteger(quantity) || inssuficientQuantity"
        ></v-text-field>
        <v-btn
          color="blue lighten-1 white--text"
          @click="sellStock"
          :disabled="quantity <= 0 || !Number.isInteger(quantity) || inssuficientQuantity"
        >{{ inssuficientQuantity ? 'Insuficiente ' : 'Vender '}}</v-btn>
      </v-container>
    </v-card>
  </v-flex>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  props: ['stock'],
  data () {
    return {
      quantity: 0
    }
  },
  computed: {
    inssuficientQuantity(){
      return this.quantity > this.stock.quantity
    }
  },
  methods: {
      ...mapActions({sellStockAction: 'sellStocks'}),
    sellStock () {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity,

      }
      
      //this.$store.dispatch('sellStock', order)
      this.sellStockAction(order)
      this.quantity = 0
    }
  },
}
</script>

<style>
</style>
