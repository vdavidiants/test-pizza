<template lang="pug">
ul.pizza-size__container
  li.pizza-size__item(v-for="size of sizes" :key="size.id" @click="setPizzaSize(size.id)" :class="{'pizza-size__item--selected': selectedSizeId === size.id}")
    h4.pizza-size__title.
      Size "{{size.name}}"
    span.pizza-size__price Price - {{size.price}}$
</template>

<script>
import { sizes } from '../model/data'

export default {
  data () {
    return {
      sizes
    }
  },
  props: {
    pizzaData: {
      type: Object,
      default: () => ({})
    }
  },
  computed: {
    selectedSizeId () {
      return this.pizzaData.sizeId
    }
  },
  methods: {
    setPizzaSize (id) {
      this.$emit('set-pizza-size', id)
    }
  }
}
</script>
