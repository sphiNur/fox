<script setup>
import HeaderTab from "@/components/HeaderTab.vue";
import Summary from "@/pages/Summary.vue";
import Daily from "@/pages/Daily.vue";
import {ref} from "vue";

const currentTab = ref(0); // Reactive state for the current tab index
const tabList = ['Daily', 'Summary']; // List of tabs
</script>

<template>
  <header>
    <HeaderTab v-model="currentTab" :tabs="tabList"/>
  </header>

  <br/>

  <main>
    <Daily v-if="currentTab === 0"/>
    <Summary v-if="currentTab === 1"/>
  </main>
</template>

<style scoped>

</style>
