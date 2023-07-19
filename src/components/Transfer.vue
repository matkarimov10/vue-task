<script setup>
import DoubleLeft from "../assets/icons/DoubleLeft.vue";
import Left from "../assets/icons/Left.vue";
import DoubleRight from "../assets/icons/DoubleRight.vue";
import Right from "../assets/icons/Right.vue";
import {ref} from "vue";


const leftSide = ref([
  {id:1, name: 'List Item 1'},
  {id:2, name: 'List Item 2'},
  {id:3, name: 'List Item 3'},
  {id:4, name: 'List Item 4'},
  {id:5, name: 'List Item 5'},
])
const rightSide = ref([
  {id:1, name: 'List Item 6'},
  {id:2, name: 'List Item 7'},
  {id:3, name: 'List Item 8'},
  {id:4, name: 'List Item 9'},
  {id:5, name: 'List Item 10'},
])


const selectedLeftItems = ref([])
const selectedRightItems = ref([])

const moveToRight = () => {
  const selectedItems = [...selectedLeftItems.value];
  leftSide.value = leftSide.value.filter(item => !selectedItems.includes(item));
  rightSide.value.push(...selectedItems);
  selectedLeftItems.value = [];
};

const moveAllToLeft = () => {
  leftSide.value.push(...rightSide.value);
  rightSide.value = [];
  selectedRightItems.value = [];
  selectedLeftItems.value = [];
};

const moveToLeft = () => {
  const selectedItems = [...selectedRightItems.value];
  rightSide.value = rightSide.value.filter(item => !selectedItems.includes(item));
  leftSide.value.push(...selectedItems);
  selectedRightItems.value = [];
};

const moveAllToRight = () => {
  rightSide.value.push(...leftSide.value);
  leftSide.value = [];
  selectedLeftItems.value = [];
  selectedRightItems.value = [];
};

const selectLeftItem = (item) => {
  if (isSelectedLeft(item)) {
    selectedLeftItems.value = selectedLeftItems.value.filter((selectedItem) => selectedItem !== item);
  } else {
    selectedLeftItems.value.push(item);
  }
};

const selectRightItem = (item) => {
  if (isSelectedRight(item)) {
    selectedRightItems.value = selectedRightItems.value.filter((selectedItem) => selectedItem !== item);
  } else {
    selectedRightItems.value.push(item);
  }
};

const isSelectedLeft = (item) => selectedLeftItems.value.includes(item);
const isSelectedRight = (item) => selectedRightItems.value.includes(item);

</script>

<template>
<div class="container my-16 mx-auto">
  <div class="flex flex-row justify-center">
    <div class="basis-1/4 border rounded-md shadow-xl p-4 m-2 w-full">
      <ul class="max-w-xs flex flex-col overflow-y-auto max-h-64" >
        <li v-for="item in leftSide" :key="item.id" @click="selectLeftItem(item)" :class="{ 'selected-item': isSelectedLeft(item) }"
            class="inline-flex items-center gap-x-2 py-3 px-4 text-sm font-medium bg-white hover:bg-gray-200 hover:cursor-pointer text-gray-900 -mt-px">
          <input :id="item.id" type="checkbox" :value="item"  v-model="selectedLeftItems"
                 class="w-6 h-6 text-blue-600 bg-gray-100 border-gray-300 ">
          <label :for="item.id" class="w-full ml-2 text-sm font-medium text-gray-900">{{item.name}}</label>
        </li>
      </ul>
    </div>


    <div class="basis-1/7 p-4 m-2">
      <div class="max-w-xs flex items-center py-6 flex-col">
        <button @click="moveAllToRight" class="p-2 border m-2 px-6 border-blue-600 rounded hover:bg-blue-50"><DoubleRight class="text-blue-900"/></button>
        <button :class="{ 'disabled border-blue-600': selectedLeftItems.length > 0 }" @click="moveToRight"
                class="p-2 border m-2 px-6 rounded hover:bg-blue-50"><Right :class="{ 'text-blue-900': selectedLeftItems.length === 1 }"/></button>
        <button :class="{ 'disabled border-blue-600': selectedRightItems.length > 0 }" @click="moveToLeft"
                class="p-2 border m-2 px-6  rounded hover:bg-blue-50"><Left :class="{ 'text-blue-900': selectedRightItems.length === 1 }"/></button>
        <button @click="moveAllToLeft" class="p-2 border m-2 px-6 border-blue-600 rounded hover:bg-blue-50"><DoubleLeft class="text-blue-900"/></button>
      </div>
    </div>


    <div class="basis-1/4 border rounded-md shadow-xl p-4 m-2 w-full">
      <ul class="max-w-xs flex flex-col overflow-y-auto max-h-60" >
        <li v-for="item in rightSide" :key="item.id" :class="{ 'selected-item': isSelectedRight(item) }"
            @click="selectRightItem(item)"
            class="inline-flex items-center gap-x-2 py-3 px-4 text-sm font-medium bg-white hover:bg-gray-200 hover:cursor-pointer text-gray-900 -mt-px">
          <input :id="item.id" type="checkbox" :value="item" v-model="selectedRightItems" class="w-6 h-6 text-blue-600 bg-gray-100 border-gray-300 ">
          <label :for="item.id" class="w-full ml-2 text-sm font-medium text-gray-900">{{item.name}}</label>
        </li>
      </ul>
    </div>

  </div>
</div>
</template>

<style scoped>

</style>