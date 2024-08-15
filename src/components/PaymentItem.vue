<script setup>
defineProps({
  onClick: {
    type: Function,
    required: true
  },
  btnName: {
    type: String,
    required: true
  },
  isEditable: {
    type: Boolean,
    default: true
  }
});
</script>

<template>
  <div>
    <input type="text" class="input input-bordered" placeholder="Name" />
    <input type="number" class="input input-bordered" disabled="{{isEditable}}" placeholder="Price" />
    <button class="btn" @click="onClick">{{ btnName }}</button>
  </div>
</template>

<style scoped>
input {
  width: 42%;
}
button {
  width: 16%;
  background-color: oklch(var(--pc));
  color: oklch(var(--b1))
}
</style>