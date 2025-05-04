<script lang="ts" setup>
import { defineProps, ref, computed } from "vue";
import { RouterLink } from "vue-router";
interface Job {
  type: string;
  title: string;
  description: string;
  salary: string;
  location: string;
  id: number;
}
// Define props with TypeScript using defineProps
// The job prop is expected to be of type Job (interface defined above)
// This syntax is specific to Vue 3's script setup
const props = defineProps<{
  job: Job;
}>();

// In vue 2 we used to define props like this:
// defineProps({
//   job: {
//     job: Object,
//   },
// });
// In vue 3 we can use defineProps to define props in a more concise way
// and we can also use TypeScript to define the type of the props.
// This is a new feature in Vue 3 that makes it easier to work with TypeScript
// and props.

const showFullDescription = ref(false);

const toggleFullDescription = () => {
  showFullDescription.value = !showFullDescription.value;
};
/*
 * Computed properties in Vue are like "smart variables" that automatically update
 * when their dependencies change. They:
 * 1. Cache their results until a dependency changes
 * 2. Only recalculate when needed (reactive)
 * 3. Are perfect for transforming or filtering data
 *
 * In this case, this computed property watches props.job.description and
 * showFullDescription, and updates the truncated text whenever they change.
 */
const truncatedDescription = computed(() => {
  let description = props.job.description;
  if (!showFullDescription.value) {
    description = description.substring(0, 90) + "...";
  }
  return description;
});
</script>

<template>
  <div class="bg-white rounded-xl shadow-md relative">
    <div class="p-4">
      <div class="mb-6">
        <div class="text-gray-600 my-2">{{ job.type }}</div>
        <h3 class="text-xl font-bold">{{ job.title }}</h3>
      </div>

      <div class="mb-5">
        <div>{{ truncatedDescription }}</div>
        <button
          @click="toggleFullDescription"
          class="text-green-500 hover:text-green-600 mb-5"
        >
          {{ showFullDescription ? "Less" : "More" }}
        </button>
      </div>

      <h3 class="text-green-500 mb-2">{{ job.salary }}</h3>

      <div class="border border-gray-100 mb-5"></div>

      <div class="flex flex-col lg:flex-row justify-between mb-4">
        <div class="text-orange-700 mb-3">
          <i class="pi pi-map-marker text-orange-700"></i>
          {{ job.location }}
        </div>
        <RouterLink
          :to="'/jobs/' + job.id"
          class="h-[36px] bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-lg text-center text-sm"
        >
          Read More
        </RouterLink>
      </div>
    </div>
  </div>
</template>
