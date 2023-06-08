<template>

    <div class="payments-item">
        <div class="payments-item__date"><span>Дата: </span>{{ payment.date }}</div>
        <div class="payments-item__title"><span>Наименование: </span>{{ payment.title }}</div>
        <div class="payments-item__summ"><span>Сумма: </span> {{ payment.summ }}</div>
        <MyButton :disabled="false" @click="showModal">Подробнее</MyButton>
    </div>

  <Modal :visible="isModalVisible" @close="closeModal">
    <template v-slot:header>
      <h3>Информация по платежу</h3>
    </template>
    <template v-slot:body>
      <ul class="payment-info">
        <li>ID: <strong>{{ payment.id}}</strong></li>
        <li>Наименование: <strong>{{ payment.title}}</strong></li>
        <li>Информация: <strong>{{ payment.desc}}</strong></li>
        <li>Сумма: <strong>{{ payment.summ }}</strong></li>
        <li>Аккаунт ID: <strong>{{ payment.account}}</strong></li>
      </ul>
    </template>
    <template v-slot:footer>
      <MyButton :disabled="false" :size="'small'" @click="closeModal">Закрыть</MyButton>
    </template>
  </Modal>
</template>

<script>
import MyButton from "@/components/common/UI/MyButton";
import Modal from "@/components/common/MyModal";

export default {
  name: "payment-item",
  props: {
    payment: {
      type: Object,
      default: () => {},
    },
  },
  components: {
    MyButton,
    Modal,
  },
  data() {
    return {
      isModalVisible: false,
    };
  },
  methods: {
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.payments-item {
  display: grid;
  grid-template-columns: 0.5fr 1fr 0.5fr 0.5fr;
  grid-template-rows: auto;
  column-gap: 1rem;
  align-items: center;
  span {
    display: none;
  }
  @media only screen and (max-width: 600px) {
    grid-template-columns: auto;
    grid-template-rows: auto auto;
    row-gap: 0.5rem;
    span {
      display: inline-block;
      font-weight: normal;
    }
    &__date {
    font-size: 15px;
    font-weight: bold;
  }
  &__summ {
    font-weight: bold;
  }
  &__title {
    font-weight: bold;
  }
  }
  
}

.payment-info {
  list-style-type: none;
  padding: 0;
  margin: 0;
}
</style>