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

async function onSubmit() {
  // toast.value.status = Object.values(data.value).some(value => typeof value === 'number' || isNaN(value));
  const body = JSON.stringify({
    bank: data.value.bank,
    payment: data.value.payment,
    salary: data.value.salary,
    market: data.value.market,
    bank_cash: data.value.bank_cash,
    cash: data.value.cash
  })
  await fetchData(body)
}

const fetchData = async (body) => {

  console.log(body);
  try {
    const res = await fetch(`https://grammybot.sphinxr.workers.dev/api/post/673/demo`, {
      method: "POST",
      body: body
    });

    const data = await res.json();

    console.log(data)
  } catch (err) {
    console.log(err);
  }
}
</script>

<template>
  <main>
    <div v-for="(value, key) in data" :key="key">
      <TextFiled v-model="data[key]" :name="key.charAt(0).toUpperCase() + key.slice(1)" />
    </div>
    <br/>
    <div class="flex flex-row w-full">
      <button class="btn w-1/2" @click="onSubmit">Submit</button>
      <input class="w-1/2" type="date">
    </div>

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
