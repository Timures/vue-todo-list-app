<template>
  <transition name="modal">
    <div
      v-if="visible"
      class="modal-mask"
      @click="close"
    >
      <div
        class="modal-wrapper"
        @click.stop
      >
        <div class="modal-container">
          <div class="modal-header">
            <slot name="header">
              <h3 class="modal-title">
                {{ title }}
              </h3>
            </slot>
          </div>
          <div class="modal-body">
            <slot name="body" />
          </div>
          <div class="modal-footer">
            <slot name="footer">
              <button
                class="modal-button"
                @click="close"
              >
                Закрыть
              </button>
            </slot>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'MyModal',
  props: {
    title: {
      type: String,
      default: 'Модальное окно',
    },
    visible: {
      type: Boolean,
      default: false,
    },
  },
  emits:['close'],
  methods: {
    close() {
      this.$emit('close');
    },
  },
};
</script>

<style>
.modal-mask {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-wrapper {
  @media only screen and (max-width: 600px) {
    width: auto;
  }
  width: 500px;
  background-color: white;
  border-radius: 4px;
}

.modal-container {
  padding: 20px;
}

.modal-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 10px;
  border-bottom: 1px solid #2c3e50;
}

.modal-title {
  margin: 0;
}

.modal-body {
  margin-bottom: 10px;
}

.modal-footer {
  border-top: 1px solid #2c3e50;
  padding-top: 1rem;
  display: flex;
  align-items: center;
  justify-content: flex-end;
}

.modal-button {
  padding: 6px 12px;
  border: none;
  background-color: #007bff;
  color: white;
  border-radius: 4px;
  cursor: pointer;
}
</style>
