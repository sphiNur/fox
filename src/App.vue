<script setup>
import TextFiled from "@/components/TextFiled.vue";
import {ref} from "vue";

const data = ref({
  bank: 0,
  payment: 0,
  salary: 0,
  market: 0,
  bank_cash: 0,
  cash: 0,
});

const toast = ref({
  class: "alert alert-info",
  status: false,
  msg: "toast",
})

function onSubmit() {
  // toast.value.status = Object.values(data.value).some(value => typeof value === 'number' || isNaN(value));
}
</script>

<template>
  <main>
    <div v-for="(value, key) in data" :key="key">
      <TextFiled v-model="data[key]" :name="key.charAt(0).toUpperCase() + key.slice(1)" />
    </div>
    <br/>
    <button class="btn" @click="onSubmit">Submit</button>

    <div class="toast" v-if="toast.status">
      <div :class="toast.class">
        <span>{{ toast.msg }}</span>
      </div>
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }
}
</style>
