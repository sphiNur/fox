<script setup>
import {ref} from "vue";
import TextFiled from "@/components/TextFiled.vue";

const data = ref({
  bank: 0,
  payment: 0,
  salary: 0,
  market: 0,
  bank_cash: 0,
  cash: 0,
});

const date = ref('')
const modal_box_status = ref(true)
const modal_box_title = ref('')
const modal_box_content = ref('')
let timeoutId = null

async function onSubmit() {
  modal_box_status.value = true

  const dataContent = Object.values(data.value).some(value => typeof value !== 'number' || isNaN(value) || /^[+-]?\d+(\.\d+)?$/.test(value.toString()));
  console.log(dataContent);

  const body = JSON.stringify({
    bank: data.value.bank,
    payment: data.value.payment,
    salary: data.value.salary,
    market: data.value.market,
    bank_cash: data.value.bank_cash,
    cash: data.value.cash,
    date: date.value,
  })

  if (date.value.length !== 0) {
    timeoutId = setTimeout( async () => {
      await fetchData(body)
    })
  } else if(dataContent) {
    modal_box_status.value = false
    modal_box_title.value = "Notice"
    modal_box_content.value = "Please just type the number."
  } else {
    modal_box_status.value = false
    modal_box_title.value = "Notice"
    modal_box_content.value = "Date is invalid, please select a date."
  }
}

const fetchData = async (body) => {
  try {
    const res = await fetch(`https://grammybot.sphinxr.workers.dev/api/post/demo`, {
      method: "POST",
      body: body
    });
    const data = await res.json();
    if (data.message === 'Success') {
      clearTimeout(timeoutId.value)
      modal_box_status.value = false
      modal_box_title.value = "Success"
      modal_box_content.value = "Pales check summary page."
    } else {
      modal_box_status.value = false
      modal_box_title.value = "Field"
      modal_box_content.value = "Failed response."
    }
  } catch (err) {
    clearTimeout(timeoutId); // Ensure timeout is cleared on error
    modal_box_status.value = false; // Hide loading spinner
    modal_box_title.value = "Error";
    modal_box_content.value = "An error occurred. Please try again.";
  }
}
</script>

<template>
  <div v-for="(value, key) in data" :key="key">
    <TextFiled v-model="data[key]" :name="key.charAt(0).toUpperCase() + key.slice(1)" />
  </div>
  <br/>
  <div class="flex flex-row w-full">
    <input class="w-1/2" type="date" v-model="date" placeholder="select date" />
    <button class="btn w-1/2" @click="onSubmit" onclick="my_modal_5.showModal()">Submit</button>
  </div>

  <!-- Open the modal using ID.showModal() method -->
  <dialog id="my_modal_5" class="modal modal-bottom sm:modal-middle">
    <div class="modal-box">
      <div class="modal-content" v-show="modal_box_status === false">
        <h3 class="text-lg font-bold">{{modal_box_title}}</h3>
        <p class="py-4">{{modal_box_content}}</p>
        <div class="modal-action">
          <form method="dialog">
            <!-- if there is a button in form, it will close the modal -->
            <button class="btn">Close</button>
          </form>
        </div>
      </div>
      <div class="modal-load" v-show="modal_box_status === true">
        <span class="loading loading-infinity loading-lg"></span>
      </div>
    </div>
  </dialog>
</template>

<style scoped>
.modal-load {
  display: flex;
  justify-content: center; /* 水平居中 */
  align-items: center;     /* 垂直居中 */
}
</style>