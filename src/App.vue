<template lang="pug">
div.container
  h1 Pizza Menu
  button(@click="setStep(0)" v-if="step < 0") Start creating your pizza
  p(v-if="step >= 0 && step < stepsOrder.length - 2") Step {{step + 1}}
  component(:is="stepsOrder[step]" :key="stepsOrder[step]" @set-pizza-size="setPizzaSize" @set-topping-id="setTopping" @set-customer-data="setCustomerData" :pizza-data="pizzaData")
  div.buttons__container(v-if="step >= 0 && step < stepsOrder.length - 1")
    button.buttons__item(@click="setStep(step-1)" v-if="step !== 0") Previous step
    button.buttons__item(@click="setStep(step+1)" v-if="step < stepsOrder.length - 1" :disabled="isDisabledNextStep") Next step
</template>

<script>
import StepPizzaSize from './components/StepPizzaSize.vue'
import StepChooseTopping from './components/StepChooseTopping.vue'
import StepCustomerDetails from './components/StepCustomerDetails.vue'
import OrderSummary from './components/OrderSummary.vue'

export default {
  data () {
    return {
      step: -1,
      pizzaData: {
        sizeId: -1,
        toppingIds: [],
        customerData: {
          name: '',
          address: '',
          phone: ''
        }
      },
      stepsOrder: [
        'StepPizzaSize',
        'StepChooseTopping',
        'StepCustomerDetails',
        'OrderSummary'
      ]
    }
  },
  components: {
    StepPizzaSize,
    StepChooseTopping,
    StepCustomerDetails,
    OrderSummary
  },
  computed: {
    isDisabledNextStep () {
      if (this.step === 0 && this.pizzaData.sizeId === -1) return true
      if (this.step === 1 && !this.pizzaData.toppingIds.length) return true
      if (this.step === 2 && Object.values(this.pizzaData.customerData).some(text => !text)) return true
      return false
    }
  },
  methods: {
    setStep (step) {
      this.step = step
    },
    setPizzaSize (id) {
      this.pizzaData.sizeId = id
    },
    setTopping (id) {
      const index = this.pizzaData.toppingIds.indexOf(id)
      if (index >= 0) {
        this.pizzaData.toppingIds.splice(index, 1)
      } else {
        this.pizzaData.toppingIds.push(id)
      }
    },
    setCustomerData (data) {
      this.pizzaData.customerData = data
    }
  }
}
</script>
