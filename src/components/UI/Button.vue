<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>


export default {
  name: "Button"
}
</script>

<style>
.btn {
  max-width: 150px;
  height: 40px;
  width: 100%;
  background-color: coral;
  color: #fff;
  border: none;
  border-radius: 30px;
  cursor: pointer;
  font-size: 16px;
}
</style>