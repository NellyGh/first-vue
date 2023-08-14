<template>
  <input :value="modelValue" @input="updateInput" class="inp" type="text" />
</template>

<script>


export default {
  name: 'Input',
  props: {
    modelValue: [String, Number]
  },
  methods: {
    updateInput(event) {
      this.$emit("update:modelValue", event.target.value)
    }
  }

}
</script>

<style>
.inp {
  max-width: 350px;
  width: 100%;
  padding: 10px;
  height: 40px;
  border: 1px solid coral;
  border-radius: 30px;
}
</style>