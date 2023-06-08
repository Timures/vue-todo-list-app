<template>
  <label :class="['checkbox', { checked: checked }, { completed: status}]">
    <input
      type="checkbox"
      :checked="checked"
      :disabled="disabled"
      @change="toggleChecked"
    >
    <span class="checkmark" />
    <slot />
  </label>
</template>

<script>
export default {
  props: {
    checked: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  emits: ['update:checked'],
  data(){
    return {
        status: false
    }
  },
  methods: {
    toggleChecked() {
      if (!this.disabled) {
        this.status = !this.status
        this.$emit('update:checked', !this.checked);
      }
    }
  }
};
</script>

<style scoped>
.checkbox {
  display: inline-block;
  position: relative;
  padding-left: 24px;
  cursor: pointer;
}

.checkbox input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
}

.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  width: 18px;
  height: 18px;
  border: 1px solid #ccc;
  background-color: #fff;
}

.checkbox:hover input ~ .checkmark {
  background-color: #f2f2f2;
}

.checkbox input:checked ~ .checkmark {
  background-color: #2196f3;
}

.checkbox input:checked ~ .checkmark:after {
  display: block;
}

.checkbox .checkmark:after {
  content: '';
  position: absolute;
  display: none;
}

.checkbox input:disabled ~ .checkmark {
  opacity: 0.6;
  pointer-events: none;
}
</style>
