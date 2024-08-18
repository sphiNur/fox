<script setup>
import {onMounted, ref} from 'vue';

const data = ref([]); // Define a ref to store the fetched data

// Define an async function to fetch data
const fetchData = async () => {
  try {
    const response = await fetch("https://grammybot.sphinxr.workers.dev/api/get/demo", {
      method: "GET",
    });

    data.value = await response.json(); // Assign the fetched data to the ref
    // Assuming insert_date is in ISO format or another valid date string format
    data.value.sort((a, b) => {
      const dateA = new Date(a.insert_date); // Parse date for item a
      const dateB = new Date(b.insert_date); // Parse date for item b
      return dateA - dateB; // Compare dates to sort in ascending order
    });
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};

// Fetch data when the component is mounted
onMounted(fetchData);
</script>

<template>
  <div class="overflow-x-auto">
    <table class="table table-xs table-pin-rows table-pin-cols">
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
      <tr v-for="(item, index) in data" :key="index">
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
</template>

<style scoped>

</style>