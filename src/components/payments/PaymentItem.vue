<template>
  <div>
    <button @click="showModal">
        <span>{{ payment.date }}</span>
        <span>{{ payment.title }}</span>
    </button>
    
  </div>

  <Modal :visible="isModalVisible" @close="closeModal">
    <template v-slot:header>
      <h3>Информация по платежу</h3>
    </template>
    <template v-slot:body>
      <ul>
        <li>{{ payment.id}}</li>
        <li>{{ payment.title}}</li>
        <li>{{ payment.desc}}</li>
        <li>{{ payment.account}}</li>
      </ul>
    </template>
    <template v-slot:footer>
      <button @click="closeModal">Закрыть</button>
    </template>
  </Modal>
</template>

<script>
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
