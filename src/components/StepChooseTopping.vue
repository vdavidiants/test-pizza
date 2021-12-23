<template lang="pug">
ul.topping__container
  li.topping__item(v-for="item of toppings" :key="item.id" @click="setTopping(item.id)" :class="{'topping__item--selected': selectedToppingId.includes(item.id), 'topping__item--full': pizzaData.toppingIds.length === 6, 'topping__item--forbidden': isForbiddenToOrder(item.id)}")
    h4.topping__title.
      "{{item.name}}"
    span.topping__price Price - {{item.price}}$
</template>

<script>
import { toppings } from '../model/data'

export default {
  data () {
    return {
      toppings
    }
  },
  props: {
    pizzaData: {
      type: Object,
      default: () => ({})
    }
  },
  computed: {
    selectedToppingId () {
      return this.pizzaData.toppingIds
    }
  },
  methods: {
    setTopping(id) {
      this.$emit('set-topping-id', id)
    },
    isForbiddenToOrder(id) {
      if(id === 4 && this.pizzaData.toppingIds.includes(5)) return true
      if(id === 5 && this.pizzaData.toppingIds.includes(4)) return true
      return false
    }
  }
}
</script>
