<script setup>
import PaymentItem from "@/components/PaymentItem.vue";
import {ref} from "vue";

function onAddClick(event) {
  console.log('onAddClick', event)
}

function onRemoveClick(event) {
  console.log('onRemoveClick', event)
}

defineProps({
  name: String
})

const formFields = ref([
  { id: 'name', type: 'text', label: 'Name', value: '' },
  { id: 'age', type: 'number', label: 'Age', value: '' },
]);
</script>

<template>
  <div class="collapse bg-base-200">
    <input type="checkbox" />
    <div class="collapse-title font-medium">
      <div class="flex flex-row w-full">
        <div class="w-1/2">{{name}}</div>
        <div class="w-1/2">price</div>
      </div>
    </div>
    <div class="collapse-content">
      <PaymentItem :on-click="onAddClick" btn-name="Add" :is-editable="true"/>

      <br />

      <div v-for="(field, index) in formFields" :key="index">
        <PaymentItem :on-click="onRemoveClick" btn-name="Rem" :is-editable='true'/>
      </div>

    </div>
  </div>
</template>

<style scoped>

</style>