<template>
    <button :class="['button', variant, size, { disabled }]" :disabled="disabled">
      <slot></slot>
    </button>
  </template>
  
  <script>
  export default {
    name: 'MyButton',
    props: {
      variant: {
        type: String,
        default: 'primary',
        validator: (value) => {
          return ['primary', 'secondary', 'success', 'danger'].includes(value);
        }
      },
      size: {
        type: String,
        default: 'medium',
        validator: (value) => {
          return ['small', 'medium', 'large'].includes(value);
        }
      },
      disabled: {
        type: Boolean,
        default: false
      }
    }
  };
  </script>
  
  <style scoped>
  .button {
    display: inline-block;
    padding: 10px 20px;
    border-radius: 4px;
    font-size: 14px;
    font-weight: bold;
    text-align: center;
    cursor: pointer;
  }
  
  .primary {
    background-color: #3f9cd1;
    color: #fff;
  }
  
  .secondary {
    background-color: #ccc;
    color: #fff;
  }
  
  .success {
    background-color: #4caf50;
    color: #fff;
  }
  
  .danger {
    background-color: #f44336;
    color: #fff;
  }
  
  .small {
    padding: 5px 10px;
    font-size: 12px;
  }
  
  .large {
    padding: 15px 30px;
    font-size: 18px;
  }
  
  .disabled {
    opacity: 0.6;
    pointer-events: none;
  }
  </style>
  