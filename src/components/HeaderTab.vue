<script setup>
import { ref, defineEmits, defineProps, watch } from 'vue';

const props = defineProps({
  tabs: {
    type: Array,
    required: true
  },
  modelValue: {
    type: Number,
    default: 0
  }
});

const emit = defineEmits(['update:modelValue']);

const activeTab = ref(props.modelValue);

// Watch for changes in the modelValue prop
watch(() => props.modelValue, (newVal) => {
  activeTab.value = newVal;
});

function onTabChanged(index) {
  activeTab.value = index;
  emit('update:modelValue', index);
}
</script>

<template>
  <div role="tablist" class="tabs tabs-boxed">
    <a
        v-for="(tab, index) in tabs"
        :key="index"
        role="tab"
        class="tab"
        :class="{ 'tab-active': activeTab === index }"
        @click="onTabChanged(index)"
    >
      {{ tab }}
    </a>
  </div>
</template>

<style scoped>

</style>