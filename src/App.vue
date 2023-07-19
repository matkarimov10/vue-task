<script setup>

import Tabs from "./components/Tabs.vue";
import AutoComplete from "./components/AutoComplete.vue";
import Transfer from "./components/Transfer.vue";
import TransferList from "./components/TransferList.vue";


const  props = defineProps(['foo'])
console.log(props.foo)

</script>

<template>
  <Tabs/>

  <AutoComplete/>

  <Transfer/>

<TransferList/>



</template>

<style scoped>

</style>
