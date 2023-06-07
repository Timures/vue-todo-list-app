<template>
  <main class="container payments">
    <h1>Платежи</h1>
    <PaymentsList :payments="payments" />
  </main>
</template>

<script>
import paymentList from '@/assets/data/payments.js'
import PaymentsList from '@/components/payments/PaymentsList'
export default {
  name: "PaymentsView",
  components: { 
    PaymentsList
  },
  data(){
    return {
      payments: paymentList
    }
  }
};
</script>