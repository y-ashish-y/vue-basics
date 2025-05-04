<script setup lang="ts">
import JobData from "@/jobs.json";
import { ref } from "vue";
import JobListingSingular from "@/components/JobListingSingular.vue";

const jobs = ref(JobData);
// when using ref, we need to use .value to access the value
console.log(jobs.value);

interface showButton {
  type: boolean;
  default: boolean;
}

defineProps<{
  limit: number;
  showButton: showButton["type"];
}>();
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
          v-for="job in jobs.splice(0, limit)"
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
