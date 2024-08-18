<script setup>
import {ref, watch} from "vue";

const props = defineProps({
  name: {
    type: String,
    required: true
  },
  modelValue: {
    type: Number,
    required: true
  }
});

const emit = defineEmits(['update:modelValue']);

const input = ref(props.modelValue);

watch(input, (newValue) => {
  emit('update:modelValue', newValue);
});
</script>

<template>
  <label class="input input-bordered flex items-center gap-2">
    {{ name }}
    <input
        type="number"
        class="grow"
        v-model="input"
    />
  </label>
</template>

<style scoped>
label {
  margin-bottom: 0.3rem;
}
</style>