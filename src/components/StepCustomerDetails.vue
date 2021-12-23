<template lang="pug">
div.contact-form
  label.contact-form__item
    p Name:
    input(type="text" v-model="customerData.name")
  label.contact-form__item
    p Address:
    input(type="text" v-model="customerData.address")
  label.contact-form__item
    p Phone:
    input(type="phone" v-model="customerData.phone")
</template>

<script>
export default {
  data () {
    return {
      customerData: {
        name: '',
        address: '',
        phone: ''
      }
    }
  },
  props: {
    pizzaData: {
      type: Object,
      default: () => ({})
    }
  },
  created () {
    this.customerData = {...this.defaultData}
  },
  computed: {
    defaultData () {
      return this.pizzaData.customerData
    }
  },
  watch: {
    customerData: {
      handler (val) {
        this.$emit('set-customer-data', val)
      },
      deep: true
    }
  }
}
</script>
