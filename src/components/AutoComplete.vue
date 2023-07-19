<script setup>
import {ref, computed} from 'vue';

const cities = ref([
  {name: 'Tashkent', population: '1.5mln'},
  {name: 'Rim', population: '10.5mln'},
  {name: 'Madrid', population: '15mln'},
  {name: 'Tokio', population: '20mln'},
  {name: 'London', population: '30mln'},
  {name: 'Moscow', population: '50mln'},
])

const searchCity = ref('');
const showList = ref(false);

const filteredCities = computed(() =>
    cities.value.filter(
        (city) =>
            city.name.toLowerCase().indexOf(searchCity.value.toLowerCase()) !== -1
    )
);


const selectCity = (city) => {
  searchCity.value = city.name;
  showList.value = false;
};


</script>

<template>
  <form class="mx-72 mt-12 flex items-center">
    <div class="relative w-full">
      <input
          v-model="searchCity"
          @focus="showList = true"
          type="text"
          id="simple-search"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg w-full pl-4 p-2.5"
          placeholder="Search..."
          required
      />

      <ul v-if="showList && filteredCities.length" class="absolute bg-white border border-gray-300 rounded-lg mt-1 w-full">
        <li
            v-for="(city, index) in filteredCities"
            :key="index"
            @click="selectCity(city)"
            class="px-4 py-2.5 cursor-pointer hover:bg-gray-100"
        >
          {{ city.name }}
        </li>
      </ul>
    </div>
  </form>

</template>

<style scoped>

</style>