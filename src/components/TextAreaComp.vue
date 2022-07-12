<template>
  <textarea cols="30" rows="10" :name="name" placeholder="Введите описание товара" @input="this.showText">

  </textarea>
</template>

<script>
  export default {
    name: 'TextAreaComp',
    props: {
      name: String,
      modelValue: String,
      updateModelValue: Function,
    },
    methods: {
      showText(evt) {
        this.$emit('update:modelValue', evt.target.value, evt.target.name);
      }
    }
  }
</script>