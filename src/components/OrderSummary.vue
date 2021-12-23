<template lang="pug">
div.summary__container
  h2.summary__title Order Summary
  p Name: {{pizzaData.customerData.name}}
  p Address: {{pizzaData.customerData.address}}
  p Phone number: {{pizzaData.customerData.phone}}
  p Total price: {{getOrderPrice}}
</template>

<script>
import { sizes, toppings } from '../model/data'

export default {
  props: {
    pizzaData: {
      type: Object,
      default: () => ({})
    }
  },
  computed: {
    getOrderPrice () {
      const pizzaPrice = sizes.find(item => item.id === this.pizzaData.sizeId).price
      const toppingsPrice = this.getToppingsPrice()
      return pizzaPrice + toppingsPrice
    }
  },
  methods: {
    getToppingsPrice () {
      const prices = this.pizzaData.toppingIds.map(id => toppings.find(item => item.id === id).price)
      if (prices.length === 3) {
        prices.sort().reverse().splice(-1, 1)
      } else if (prices.length === 6) {
        prices.sort().reverse().splice(-2, 2)
      }
      return prices.reduce((sum, item) => sum + item, 0)
    }
  }
}
</script>
