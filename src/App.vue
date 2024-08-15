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

function onSubmit() {
  console.log(data.value);
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
  </header>

  <main>
    <div v-for="(value, key) in data" :key="key">
      <TextFiled v-model="data[key]" :name="key.charAt(0).toUpperCase() + key.slice(1)" />
    </div>
    <br/>
    <button class="btn" @click="onSubmit">Submit</button>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
