<script setup>
import { ref, onMounted } from "vue";

const activeTab = ref(0);
const changeTab = (index) => {
  activeTab.value = index;
};

const tabs = [
  {
    slug: 'item_one',
    label: 'ITEM ONE',
    content: 'Item one'
  },
  {
    slug: 'item_two',
    label: 'ITEM TWO',
    content: 'Item two'
  },
  {
    slug: 'item_three',
    label: 'ITEM THREE',
    content: 'Item three '
  },

];

onMounted(() => {
  changeTab(0);
});
</script>

<template>
  <div class="container max-w-2xl mx-auto border-[1px] rounded-xl my-12">
    <div class="px-8">
      <ul class="mb-5 flex list-none border-b-[1px]" role="tablist">
        <li role="presentation" v-for="(tab, index) in tabs" :key="index">
          <button  :class="{
              'mr-2 block px-4 pb-2 pt-4 text-md text-blue-600 font-medium uppercase border-b-2 border-blue-500': activeTab === index,
              ' mr-2 block border-x-0 border-b-2 border-t-0 border-transparent px-4 pb-2 pt-4 text-md font-medium uppercase': activeTab !== index}"
          @click ="changeTab(index)">{{ tab.label }}</button>
        </li>
      </ul>
    </div>


    <div class="flex mb-6">
      <div class="flex-1">
        <div v-for="(tab, index) in tabs" :key="index">
         <div  v-if="activeTab===index">
           {{tab.content}}
         </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
