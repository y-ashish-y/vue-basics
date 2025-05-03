<script setup lang="ts">
defineProps({
  bg: {
    type: String,
    default: "bg-gray-100",
  },
});
</script>

<template>
  <!-- when we add : to bind the element and whatever we put in double quote is javascript -->
  <!-- :class is used to bind the class dynamically -->
  <div :class="`${bg} p-6 rounded-lg shadow-md`">
    <slot></slot>
  </div>
</template>
