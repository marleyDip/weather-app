<template>
  <Header class="sticky top-0 bg-weather-primary shadow-lg">
    <nav
      class="container flex flex-col sm:flex-row items-center gap-4 text-white py-6"
    >
      <RouterLink :to="{ name: 'home' }">
        <div class="flex items-center gap-3">
          <i class="fa-solid fa-cloud-sun text-2xl"></i>
          <p class="text-2xl">The Local Weather</p>
        </div>
      </RouterLink>

      <div class="flex gap-3 flex-1 justify-end">
        <i
          class="fa-solid fa-circle-info text-xl hover:text-weather-secondary duration-150 cursor-pointer"
          @click="toggleModal"
        ></i>

        <i
          class="fa-solid fa-plus text-xl hover:text-weather-secondary duration-150 cursor-pointer"
        ></i>
      </div>

      <!-- They bind a prop called modalActive to the value of the variable modalActive. -->
      <!--  So... why use v-bind (or :)?
      Because you're passing data (a variable) from a parent component to a child component. In this case:

      1. The parent has modalActive in its <script>

      2. You're telling the child (<BaseModal>) to receive that value as a prop -->
      <BaseModal :modalActive="modalActive" @close="toggleModal">
        <div class="text-black text-justify">
          <h1 class="text-2xl mb-1">About:</h1>
          <p class="mb-4">
            The Local Weather allows you to track the current and future weather
            of cities of your choosing.
          </p>

          <h2 class="text-2xl">How it works:</h2>
          <ol class="list-decimal list-inside mb-4">
            <li>Search for the city by entering the name into the search.</li>
            <li>
              Select the city within the results , this will take ypu to the
              current weather for your selection.
            </li>
            <li>
              Track the city by clicking on the "+" icon in the top right. this
              will save the city to view at a later time on the home page.
            </li>

            <h2 class="text-2xl">Removing a city:</h2>
            <p>
              If you no longer wish to tack a city, simply select the city
              within the home page. At the bottom of the page, there will be an
              option to delete the city.
            </p>
          </ol>
        </div>
      </BaseModal>
    </nav>
  </Header>
</template>

<script setup>
import { RouterLink } from "vue-router";
import BaseModal from "./BaseModal.vue";
import { ref } from "vue";

//In Vue 3's Composition API, we use ref() to create reactive variables — values that Vue will automatically track and update in the DOM when they change.

//ref(null) creates a reactive value starting as null.
//null = unknown / not set yet.
//ref()	To create a reactive value (number, string, boolean, etc.)
//reactive()	To make a reactive object (with multiple properties)

//his function toggles the modal open/close.
//If modalActive.value is false, it becomes true.
//If null, the first click will make it true (because !null === true).
const modalActive = ref(null);
const toggleModal = () => {
  modalActive.value = !modalActive.value;
};
</script>

<style scoped>
</style>