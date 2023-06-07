<template>
  <div class="payments-list">
    <ul>
      <li v-for="payment in payments" :key="payment.id">
        <PaymentItem :payment="payment" />
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
