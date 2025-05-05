<script setup lang="ts">
// import JobData from "@/jobs.json";
import { onMounted, reactive } from "vue";
import JobListingSingular from "@/components/JobListingSingular.vue";
import axios from "axios";

// const jobs = ref([]);
// // when using ref, we need to use .value to access the value
// console.log(jobs.value);

// ref vs reactive

// reactive() only takes objects. It does not take primitives like strings, numbers and booleans. It uses ref() under the hood.
// ref() can take objects or primitives.
// ref() has a .value property for reassigning, reactive() doesn't use .value and can't be reassigned

const state = reactive({
  jobs: [],
  isLoading: true,
});

interface showButton {
  type: boolean;
  default: boolean;
}

defineProps<{
  limit: number;
  showButton: showButton["type"];
}>();

onMounted(async () => {
  // Fetch the job data from the JSON file
  try {
    const response = await axios.get("http://localhost:5000/jobs");
    state.jobs = response.data;
  } catch (error) {
    console.error("Error fetching job data:", error);
  } finally {
    state.isLoading = false;
  }
});
</script>

<template>
  <!-- JobListing section - light blue bg, padding x-4 y-10 -->
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse Jobs
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <JobListingSingular
          v-for="job in state.jobs.splice(0, limit || state.jobs.length)"
          :key="job.id"
          :job="job"
        />
      </div>
    </div>
  </section>
  <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
    <a
      href="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs</a
    >
  </section>
</template>
