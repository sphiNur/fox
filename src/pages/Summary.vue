<script setup>
import {computed, onMounted, ref} from 'vue';

const data = ref([]); // Define a ref to store the fetched data

// Define an async function to fetch data
const fetchData = async () => {
  try {
    const response = await fetch("https://grammybot.sphinxr.workers.dev/api/get/demo",{method: "GET"});
    const jsonData = await response.json();
    jsonData.sort((a, b) => new Date(a.insert_date) - new Date(b.insert_date));
    data.value = jsonData;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};

const confirmed_data = computed(() => data.value.filter(item => item.is_confirmed === 1));
const unconfirmed_data = computed(() => data.value.filter(item => item.is_confirmed === 0));

const onConfirm = async (item) => {
  try {
    const response = await fetch(`https://grammybot.sphinxr.workers.dev/api/post/updateConfirm/demo`, {
      method: 'POST',
      body: JSON.stringify(item)
    });
    // 更新本地数据
    const jsonData = await response.json();

    if (jsonData.message.success) {
      item.is_confirmed = 1;
    } else {
      console.log(jsonData);
    }
  } catch (error) {
    console.error('更新项时出错:', error);
  }
};

// Fetch data when the component is mounted
onMounted(fetchData);
</script>

<template>
  <div class="max-h-96 overflow-x-auto">
    <table class="table table-zebra table-xs table-pin-rows table-pin-cols">
      <thead>
      <tr>
        <th>Date</th>
        <td>Bank</td>
        <td>Payment</td>
        <td>Salary</td>
        <td>Market</td>
        <td>Bank Cash</td>
        <td>Cash</td>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(item, index) in confirmed_data" :key="index">
        <th>{{ item.insert_date }}</th>
        <td>{{ item.bank }}</td>
        <td>{{ item.payment }}</td>
        <td>{{ item.salary }}</td>
        <td>{{ item.market }}</td>
        <td>{{ item.bank_cash }}</td>
        <td>{{ item.cash }}</td>
      </tr>
      </tbody>
    </table>
  </div>
  <br/>
  <div class="max-h-48 overflow-x-auto">
    <div></div>
    <table class="table table-zebra table-xs table-pin-rows table-pin-cols">
      <thead>
      <tr>
        <th>Date</th>
        <td>Bank</td>
        <td>Payment</td>
        <td>Salary</td>
        <td>Market</td>
        <td>Bank Cash</td>
        <td>Cash</td>
        <td>Confirm</td>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(item, index) in unconfirmed_data" :key="index">
        <th>{{ item.insert_date }}</th>
        <td>{{ item.bank }}</td>
        <td>{{ item.payment }}</td>
        <td>{{ item.salary }}</td>
        <td>{{ item.market }}</td>
        <td>{{ item.bank_cash }}</td>
        <td>{{ item.cash }}</td>
        <td>
          <button class="btn btn-outline btn-warning btn-xs" @click="onConfirm(item)">OK</button>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>

</style>