<template>
  <div class="w-48 h-56 overflow-auto border rounded p-2">
    <div
        v-for="item in items"
        :key="item"
        class="flex items-center mb-2"
        @click="toggle(item)"
    >
      <input type="checkbox" :checked="isChecked(item)" class="mr-2" />
      <span>List item {{ item + 1 }}</span>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    items: {
      type: Array,
      required: true,
    },
    checkedItems: {
      type: Array,
      required: true,
    },
  },
  methods: {
    toggle(item) {
      this.$emit('toggle', item);
    },
    isChecked(item) {
      return this.checkedItems.includes(item);
    },
  },
});
</script>