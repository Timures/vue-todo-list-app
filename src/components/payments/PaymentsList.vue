<template>
  <div class="payments-list">
    <div class="payments-list-header">
      <h3>Дата </h3>
      <h3>Наименование</h3>
      <h3>Сумма</h3>
      <h3>Действие</h3>
    </div>
    <ul>      
      <li v-for="payment in payments" :key="payment.id">
        <PaymentItem :payment="payment" />
        <hr />
      </li>
      
    </ul>
  </div>
</template>

<script>
import PaymentItem from "@/components/payments/PaymentItem";
export default {
  name: "payments-list",
  props: {
    payments: {
      type: Array,
      default: () => {
        [];
      },
    },
  },
  components: { PaymentItem },
};
</script>

<style lang="scss" scoped>
.payments-list {

  &-header {
    @media only screen and (max-width: 600px) {
      display: none;
    }
    display: grid;
  grid-template-columns: 0.5fr 1fr 0.5fr 0.5fr;
  grid-template-rows: auto;
  column-gap: 1rem;
  align-items: center;
  margin-bottom: 1rem;
    border-bottom: 1px solid #2c3e50;
   
  }
  ul {
    list-style-type: none;
  margin: 0;
  padding: 0;
  li {
    &:not(:last-child){
      margin-bottom: 0.5rem;
    }
  }
  }
}</style>