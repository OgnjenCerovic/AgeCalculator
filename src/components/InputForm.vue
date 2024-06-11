<template>
    <div class="form-group">
      <label :for="label">{{ label }}</label>
      <input :type="type" :id="label" v-model="inputValue"/>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      label: String,
      type: {
        type: String,
        default: 'text'
      },
      modelValue: [String, Number]
    },
    computed: {
      inputValue: {
        get() {
          return this.modelValue;
        },
        set(value) {
          this.$emit('update:modelValue', value);
        }
      }
    }
  }
  </script>